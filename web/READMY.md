### Установка(это не офийиальный пакет)официальный к сожелению потом нормально не разворачиваеться через гит и не работает... поэтому юзаем не официальную

    composer create-project drupal-composer/drupal-project:8.x-dev some-dir --stability dev --no-interaction

#### если нужен все так иофициальный тогда так
    
    composer create-project drupal/drupal . 8.@dev


#установка

    drush site-install --db-url=mysql://{username}:{password}@localhost/{database}
    drush site-install --db-url=mysql://root@localhost/drupal8_second

###Добавления в зависимость и заливка модулей (версия выбираеться через @stable @dev если не указать будет установлено ка кнастроено в лок(dev по дефолту))
#### https://getcomposer.org/doc/articles/versions.md

    composer require drupal/token @stable
    composer require drupal/metatag  @stable
    composer require drupal/pathauto @stable
    composer require drupal/panels @stable
    composer require drupal/linkit @stable
    composer require drupal/module_filter @stable
    
    composer require drupal/redirect
    composer require drupal/webform
    composer require drupal/page_manager
    composer require drupal/block_class
    composer require drupal/dropzonejs
#Включения модулей
    
    drush en token  metatag  pathauto redirect webform panels page_manager linkit module_filter dropzonejs block_class -y;


###Удаление пакетов
###Всё очень просто, выполняется это одной командой и это удаляет как прописанную зависимость, так и физически модуль. Но будьте крайне осторожны, ведь сначала надо удалить модуль из друпала, а уже затем физически.

    drush dis token  metatag  pathauto redirect webform panels page_manager block_class linkit module_filter dropzonejs -y;
    
    composer remove drupal/token 
    composer remove drupal/metatag 
    composer remove drupal/pathauto
    composer remove drupal/redirect
    composer remove drupal/webform
    composer remove drupal/panels
    composer remove drupal/page_manager
    composer remove drupal/block_class
    composer remove drupal/linkit
    composer remove drupal/module_filter
    composer remove drupal/dropzonejs
    

#НЕ ПРОБОВАЛ НО!

##Автоматическое применение патчей
##Композер, сам по себе, не умеет это делать, но есть плагин который это умеет делать.

    composer require cweagans/composer-patches

Сам патч
 
    "extra": {
        "patches": {
            "drupal/drupal": {
                "Add startup configuration for PHP server": "https://www.drupal.org/files/issues/add_a_startup-1543858-30.patch"
            }
        }
    }



##Можно создать свой композер с модулями(наработками) и подключить его через композер зависимости и юзать, например через github
    composer config repositories.restful vcs "https://github.com/RESTful-Drupal/restful"


##update drupal/core
    composer update drupal/core
    drush updatedb

##update module
    composer update drupal/devel
    drush updatedb

## перенос
    git clone https://github.com/serjsv87/drupal8-test
##Импорт
Выгрузка данных

    drush config-export 

или

    drush cex

git всего и на сайте принимания выполняем команду

    drush config-import --preview=diff

или

    drush cim



##Когда тестил столкнулся с проблемой
Site UUID in source storage does not match the target storage.
##лечиться установкой аналогичного ключа, 

####получить ключ командой

    drush config-get "system.site" uuid

####Установить ключ командой

    drush config-set "system.site" uuid "f9322262-1ccb-4e7e-a7b0-feca5497c814"

###Вторая ошибка вещала что не может засинкать шоттег решения удалить их... Как это не странно.. (

Administration > Configuration > User interface > Shortcuts (admin/config/user-interface/shortcut), than in "List links" of "Default" I deleted every shortcut.


#Создания модуля
Туториал мне понравился

https://internetdevels.ru/blog/building-drupal-8-modules-a-practical-guide
