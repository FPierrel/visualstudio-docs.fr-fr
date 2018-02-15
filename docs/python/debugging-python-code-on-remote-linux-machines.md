---
title: "Débogage de code Python sur des ordinateurs Linux distants à l’aide de Visual Studio | Microsoft Docs"
description: "Guide pratique pour utiliser Visual Studio pour déboguer du code Python exécuté sur des ordinateurs Linux distants, y compris les étapes de configuration nécessaires, la sécurité et le dépannage."
ms.custom: 
ms.date: 07/12/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-python
dev_langs:
- python
ms.tgt_pltfrm: 
ms.topic: article
author: kraigb
ms.author: kraigb
manager: ghogen
ms.workload:
- python
- data-science
ms.openlocfilehash: 11e48a67540ff7df665cc044557751be4b1c3be0
ms.sourcegitcommit: 205d15f4558315e585c67f33d5335d5b41d0fcea
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/09/2018
---
# <a name="remotely-debugging-python-code-on-linux"></a>Débogage à distance de code Python sur Linux

Visual Studio peut lancer et déboguer des applications Python localement et à distance sur un ordinateur Windows (voir [Débogage à distance](../debugger/remote-debugging.md)). Il peut également effectuer un débogage à distance sur un autre système d’exploitation, un appareil différent ou une implémentation Python autre que CPython à l’aide de la [bibliothèque ptvsd](https://pypi.python.org/pypi/ptvsd).

Lorsque vous utilisez ptvsd, le code Python faisant l’objet du débogage héberge le serveur de débogage auquel Visual Studio peut être attaché. Cet hébergement nécessite une petite modification de votre code pour importer et activer le serveur, et peut exiger des configurations du réseau ou du pare-feu sur l’ordinateur distant pour autoriser les connexions TCP.

Pour une introduction au débogage à distance, visionnez la vidéo [Deep Dive: Cross-Platform Remote Debugging](https://youtu.be/y1Qq7BrV6Cc) (youtube.com, 6 minutes 22 secondes), qui est applicable à Visual Studio 2015 et 2017.

> [!VIDEO https://www.youtube.com/embed/y1Qq7BrV6Cc]

## <a name="setting-up-a-linux-computer"></a>Configuration d’un ordinateur Linux

Les éléments suivants sont nécessaires pour suivre cette procédure pas à pas :

- Un ordinateur distant exécutant Python sur un système d’exploitation Mac OSX ou Linux.
- Un port 5678 (entrant) ouvert sur le pare-feu de cet ordinateur (paramètre par défaut pour le débogage à distance).

Vous pouvez facilement créer des [machines virtuelles Linux dans Azure](/azure/virtual-machines/linux/creation-choices) et [accéder à ces machines à l’aide du Bureau à distance](/azure/virtual-machines/linux/use-remote-desktop) de Windows. Utilisez de préférence l’interpréteur Ubuntu sur la machine virtuelle, car Python est installé par défaut. Sinon, consultez [Sélection et installation des interpréteurs Python](managing-python-environments-in-visual-studio.md#selecting-and-installing-python-interpreters) pour obtenir la liste des autres emplacements de téléchargement d’interpréteurs Python.

Pour plus d’informations sur la création d’une règle de pare-feu pour une machine virtuelle Azure, consultez [Ouverture de ports sur une machine virtuelle dans Azure à l’aide du portail Azure](/azure/virtual-machines/windows/nsg-quickstart-portal).

## <a name="preparing-the-script-for-debugging"></a>Préparation du script pour le débogage

1. Sur l’ordinateur distant, créez un fichier Python appelé `guessing-game.py` à l’aide du code suivant :

  ```python
  import random

  guesses_made = 0
  name = input('Hello! What is your name?\n')
  number = random.randint(1, 20)
  print('Well, {0}, I am thinking of a number between 1 and 20.'.format(name))

  while guesses_made < 6:
      guess = int(input('Take a guess: '))
      guesses_made += 1
      if guess < number:
          print('Your guess is too low.')
      if guess > number:
          print('Your guess is too high.')
      if guess == number:
          break
  if guess == number:
      print('Good job, {0}! You guessed my number in {1} guesses!'.format(name, guesses_made))
  else:
      print('Nope. The number I was thinking of was {0}'.format(number))
  ```
 
1. Installez le package `ptvsd` dans votre environnement à l’aide de `pip3 install ptvsd`. (Remarque : il est conseillé d’enregistrer la version du ptvsd qui est installé au cas où vous en auriez besoin pour la résolution des problèmes ; la [liste des ptvsd](https://pypi.python.org/pypi/ptvsd) indique également les versions disponibles.)

1. Activez le débogage à distance en ajoutant le code ci-dessous au premier point possible dans `guessing-game.py`, avant tout autre code. (Bien que cela ne soit pas strictement nécessaire, il est impossible de déboguer des threads en arrière-plan générés avant que la fonction `enable_attach` ne soit appelée.)

   ```python
   import ptvsd
   ptvsd.enable_attach('my_secret')
   ```

   Le premier argument passé à `enable_attach` (appelé « secret ») restreint l’accès au script exécuté. Vous entrez ce secret au moment où vous attachez le débogueur distant. (Cette pratique est déconseillée, mais vous pouvez autoriser tout le monde à se connecter, en utilisant le code `enable_attach(secret=None)`.)

1. Enregistrez le fichier et exécutez `python3 guessing-game.py`. L’appel à `enable_attach` s’exécute en arrière-plan et attend les connexions entrantes issues de vos interactions avec le programme. Si vous le souhaitez, la fonction `wait_for_attach` peut être appelée après `enable_attach` pour bloquer le programme jusqu’à ce que le débogueur soit attaché.

> [!Tip]
> En plus de `enable_attach` et `wait_for_attach`, ptvsd fournit une fonction d’assistance `break_into_debugger`, qui sert de point d’arrêt par programmation si le débogueur est attaché. Il existe également une fonction `is_attached` qui renvoie `True` si le débogueur est attaché (notez qu’il n’est pas nécessaire de vérifier ce résultat avant d’appeler d’autres fonctions `ptvsd`).

## <a name="attaching-remotely-from-python-tools"></a>Attachement à distance à partir de Python Tools

Dans ces étapes, nous allons définir un point d’arrêt simple pour arrêter le processus distant.

1. Créez une copie du fichier distant sur l’ordinateur local et ouvrez-le dans Visual Studio. L’emplacement du fichier importe peu, mais son nom doit correspondre au nom du script sur l’ordinateur distant.

1. (Facultatif) Pour activer la fonctionnalité IntelliSense pour ptvsd sur l’ordinateur local, installez le package ptvsd dans votre environnement Python.

1. Sélectionnez **Déboguer > Attacher au processus**.

1. Dans la boîte de dialogue **Attacher au processus** qui s’affiche, définissez **Type de connexion** sur **Python à distance (ptvsd)**. (Dans les versions antérieures de Visual Studio, ces commandes s’appellent **Transport** et **Débogage à distance Python**.)

1. Dans le champ **Cible de la connexion** (ou **Qualificateur** dans les versions antérieures), entrez `tcp://<secret>@<ip_address>:5678` où `<secret>` est la chaîne `enable_attach` passée dans le code Python, `<ip_address>` est celle de l’ordinateur distant (qui peut être une adresse explicite ou un nom tel que myvm.cloudapp.net) et `:5678` est le numéro du port de débogage à distance.

    > [!Warning]
    > Si vous créez une connexion sur l’Internet public, vous devez utiliser `tcps` à la place et suivre les instructions ci-dessous pour [sécuriser la connexion du débogueur avec SSL](#securing-the-debugger-connection-with-ssl).

1. Appuyez sur Entrée pour remplir la liste des processus ptvsd disponibles sur cet ordinateur :

    ![Saisie de la cible de la connexion et affichage de la liste des processus](media/remote-debugging-qualifier.png)

    Si vous démarrez un autre programme sur l’ordinateur distant après avoir rempli cette liste, sélectionnez le bouton **Actualiser**.

1. Sélectionnez le processus à déboguer, puis le bouton **Attacher**, ou double-cliquez sur le processus.

1. Visual Studio passe alors en mode débogage. Le script continue à s’exécuter sur l’ordinateur distant pour fournir toutes les fonctionnalités de [débogage](debugging-python-in-visual-studio.md) habituelles. Par exemple, définissez un point d’arrêt sur la ligne `if guess < number:`, puis basculez sur l’ordinateur distant et entrez une autre hypothèse. Après cela, Visual Studio sur votre ordinateur local s’arrête au point d’arrêt défini, affiche les variables locales, et ainsi de suite :

    ![Le point d’arrêt est atteint](media/remote-debugging-breakpoint-hit.png)

1. Quand vous arrêtez le débogage, Visual Studio se détache du programme, qui continue à s’exécuter sur l’ordinateur distant. ptvsd poursuit également l’écoute des attachements de débogueurs, pour vous permettre de rattacher le processus à tout moment.

### <a name="connection-troubleshooting"></a>Résolution des problèmes de connexion

1. Vérifiez que vous avez sélectionné **Python à distance (ptvsd)** pour **Type de connexion** (ou **Débogage à distance Python** pour **Transport** dans les versions antérieures).
1. Vérifiez que le secret dans **Cible de la connexion** (ou **Qualificateur**) est strictement identique au secret dans le code distant.
1. Vérifiez que l’adresse IP dans **Cible de la connexion** (ou **Qualificateur**) correspond à celle de l’ordinateur distant.
1. Vérifiez que vous avez ouvert le port de débogage à distance sur l’ordinateur distant et que vous avez inclus le suffixe du port, tel que `:5678`, dans la cible de la connexion.
    - Si vous devez utiliser un port différent, vous pouvez le spécifier dans l’appel à `enable_attach` avec l’argument `address`, comme ceci : `ptvsd.enable_attach(secret = 'my_secret', address = ('0.0.0.0', 8080))`. Dans ce cas, ouvrez ce port spécifique dans le pare-feu.
1. Vérifiez que la version du ptvsd installée sur l’ordinateur distant, et qui est retournée par `pip3 list`, correspond à celle utilisée par la version des outils Python utilisés dans Visual Studio, comme indiqué dans le tableau suivant. Si nécessaire, mettez à jour ptvsd sur l’ordinateur distant.

    | Version de Visual Studio | Version des outils Python/ptvsd |
    | --- | --- |
    | 2017 15.3 | 3.2.0 |
    | 2017 15.2 | 3.1.0 |
    | 2017 15.0, 15.1 | 3.0.0 |
    | 2015 | 2.2.6 |
    | 2013 | 2.2.2 |
    | 2012, 2010 | 2.1 |

## <a name="securing-the-debugger-connection-with-ssl"></a>Sécurisation de la connexion du débogueur avec SSL

Par défaut, la connexion au serveur de débogage à distance ptvsd est sécurisée uniquement par le secret, et toutes les données sont transmises en texte brut. Pour sécuriser davantage la connexion, ptvsd prend en charge SSL, que vous devez définir comme suit :

1. Sur l’ordinateur distant, générez séparément un certificat auto-signé et les fichiers de clés en utilisant openssl :

    ```command
    openssl req -new -x509 -days 365 -nodes -out cert.cer -keyout cert.key
    ```

    Quand vous y êtes invité par openssl, entrez le nom d’hôte ou l’adresse IP (selon ce que vous avez utilisé pour vous connecter) comme **nom commun**.

    (Pour plus d’informations, consultez [Certificats auto-signés](http://docs.python.org/3/library/ssl.html#self-signed-certificates) dans les documents du module `ssl` de Python. Notez que, dans ces documents, la commande crée un seul fichier combiné.)

1. Dans le code, modifiez l’appel à `enable_attach` pour inclure les arguments `certfile` et `keyfile` en utilisant les noms de fichiers comme valeurs (ces arguments ont la même signification que pour la fonction `ssl.wrap_socket` standard de Python) :

    ```python
    ptvsd.enable_attach(secret='my_secret', certfile='cert.cer', keyfile='cert.key')
    ```

    Vous pouvez également effectuer la même modification dans le fichier de code sur l’ordinateur local, mais cela n’est pas obligatoire étant donné que ce code n’est pas réellement exécuté.

1. Redémarrez le programme Python sur l’ordinateur distant, en préparation du débogage.

1. Sécurisez le canal en ajoutant le certificat à l’autorité de certification racine de confiance sur l’ordinateur Windows à l’aide de Visual Studio :

    1. Copiez le fichier de certificat de l’ordinateur distant sur l’ordinateur local.
    1. Ouvrez le Panneau de configuration et accédez à **Outils d’administration > Gérer les certificats d’ordinateur**.
    1. Dans la fenêtre qui s’affiche, développez **Autorités de certification racines de confiance** sur le côté gauche, cliquez avec le bouton droit sur **Certificats**, puis sélectionnez **Toutes les tâches > Importer...**.
    1. Accédez au fichier `.cer` copié de l’ordinateur distant et sélectionnez-le, puis cliquez successivement dans les boîtes de dialogue pour effectuer l’importation.

1. Répétez le processus d’attachement dans Visual Studio comme décrit précédemment, en spécifiant cette fois-ci le protocole `tcps://` dans **Cible de la connexion** (ou **Qualificateur**).

    ![Choix du transport de débogage à distance avec SSL](media/remote-debugging-qualifier-ssl.png)

### <a name="warnings"></a>Avertissements

Visual Studio vous avertit de problèmes de certificat potentiels quand vous vous connectez via le protocole SSL, comme décrit ci-dessous. Vous pouvez ignorer les avertissements et continuer mais, même si le canal reste chiffré contre les écoutes clandestines, il est vulnérable à des attaques de l’intercepteur.

1. Si vous recevez un avertissement du type « le certificat distant n’est pas approuvé », comme celui illustré ci-dessous, cela signifie que vous n’avez pas ajouté correctement le certificat à l’autorité de certification racine de confiance. Vérifiez ces étapes, puis réessayez.

    ![Avertissement lié au certificat SSL approuvé](media/remote-debugging-ssl-warning.png)

1. Si vous recevez un avertissement du type « le nom du certificat distant ne correspond pas au nom d’hôte », comme celui illustré ci-dessous, cela signifie que vous n’avez pas utilisé le nom d’hôte ou l’adresse IP approprié comme **nom commun** lors de la création du certificat.

    ![Avertissement lié au nom d’hôte du certificat SSL](media/remote-debugging-ssl-warning2.png)

> [!Warning]
> À l’heure actuelle, Visual Studio 2017 se bloque si vous ignorez ces avertissements. Assurez-vous de corriger tous les problèmes avant d’essayer de vous connecter.