Trucs et astuces
----------------

#. Comment créer un profil Firefox

  Utiliser Firefox pour créer un profil, cela peut être utile si vous utilisez un proxy, des add-ons, ou si vous souhaitez vous authentifier sur des sites avec des authentifications particulières (NTLM notamment).
  Lorsque votre profil est terminé, copier le dans le répertoire spécifié dans le /etc/default/selenium de votre servuer Selenium. Pour que celui-ci soit pris en compte, vider le cache et spécifier le chemin d'accès au profil dans /etc/default/selenium.

.. warning:: 
   Vérifier la taille du profil, si celle ci est trop importante, des performances dégradées sont possibles.
  
Enfin, redémarrer le serveur Selenium pour prendre en compte les modifications.

#. Désactiver les AddOns et mise-à-jour automatiques

  Parfois, la mise à jour automatique peut bloquer le navigateur et donc provoquer un timeout de votre contrôle. Pour désactiver la fonctionnalité, rendez-vous dans **Options > Avancé > Mises à jour** et décocher la case **Installer automatiquement les mises à jours**

#. Temporiser vos scénarios

  Si le site contrôlé subit des problèmes de latence, des "pauses" peuvent être ajoutées aux scénarios avec les actions **clickAndWait** ou **waitForPageToLoad**. Cela peux éviter les faux positifs sur certaines étapes de vos scnéarions.

