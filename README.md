Структура:
Корневой каталог с проектом service:
*Service
	* Source Code - обвязка для тестов
		* constant - константы для тестов
	* Test - тесты

Каждый тип набора (posts, comments, albums и т.п) описан в виде класса с одноименным название класса и файла.
Общие методы для всех классов вынесены в базовый класс Object. 
Каждый класс наследует базовый класс, некоторые классы так же дополнены дополнительными методами.

* Test
	* conftest - создается окружение для тестов, создается объект класса Jsonplaceholder.
В классе Jsonplaceholder создаются объекты всех классов

Используемые библиотеки:
- pytest
- requests
- hamcrest (реализует более удобную обработку исключений, по сравнению с assert)

Тесты запускались в следующем окружении: platform win32 -- Python 3.6.5, pytest-3.6.0, py-1.5.3, pluggy-0.6.0 -- 

**---------------------**
Для запуска тестов из cmd необходимо добавить в переменную окруженя каталоги Source Code, Test
Из каталога Test, запуск тестов с ключами python -m pytest -v

Результат запуска (PASSED - тест пройден; FAILED - тест не пройден):

============================= test session starts =============================
platform win32 -- Python 3.6.5, pytest-3.6.0, py-1.5.3, pluggy-0.6.0 -- c:\Python36\python.exe
cachedir: .pytest_cache
rootdir: d:\python\python36\LEARNING\service\Test, inifile:
plugins: allure-adaptor-1.7.10
collecting ... collected 40 items

test_albums.py::test_status[200-https://jsonplaceholder.typicode.com/albums] PASSED [  2%]
test_albums.py::test_status[404-https://jsonplaceholder.typicode.com/albums_no] PASSED [  5%]
test_albums.py::test_get_by_id PASSED                                    [  7%]
test_albums.py::test_album_create PASSED                                 [ 10%]
test_albums.py::test_album_delete PASSED                                 [ 12%]
test_comments.py::test_get_by_mail[1-Nikita@garfield.biz] PASSED         [ 15%]
test_comments.py::test_get_by_mail[1-Meghan_Littel@rene.us] PASSED       [ 17%]
test_comments.py::test_get_by_mail[0-test@test.ru] PASSED                [ 20%]
test_comments.py::test_status[200-https://jsonplaceholder.typicode.com/comments] PASSED [ 22%]
test_comments.py::test_status[200-https://jsonplaceholder.typicode.com/comments?postId=13] PASSED [ 25%]
test_comments.py::test_status[404-https://jsonplaceholder.typicode.com/comments_no] PASSED [ 27%]
test_comments.py::test_get_by_id PASSED                                  [ 30%]
test_comments.py::test_comment_create PASSED                             [ 32%]
test_comments.py::test_comment_delete PASSED                             [ 35%]
test_photos.py::test_status[200-https://jsonplaceholder.typicode.com/photos] PASSED [ 37%]
test_photos.py::test_status[404-https://jsonplaceholder.typicode.com/photos_no] PASSED [ 40%]
test_photos.py::test_get_by_id PASSED                                    [ 42%]
test_photos.py::test_photo_create FAILED                                 [ 45%]
test_photos.py::test_photo_delete PASSED                                 [ 47%]
test_posts.py::test_status[200-https://jsonplaceholder.typicode.com/posts/] PASSED [ 50%]
test_posts.py::test_status[200-https://jsonplaceholder.typicode.com/posts?userId=1] PASSED [ 52%]
test_posts.py::test_status[404-https://jsonplaceholder.typicode.com/posts_no] PASSED [ 55%]
test_posts.py::test_get_by_id PASSED                                     [ 57%]
test_posts.py::test_post_create PASSED                                   [ 60%]
test_posts.py::test_post_delete PASSED                                   [ 62%]
test_todos.py::test_status[200-https://jsonplaceholder.typicode.com/todos/] PASSED [ 65%]
test_todos.py::test_status[404-https://jsonplaceholder.typicode.com/todos_no] PASSED [ 67%]
test_todos.py::test_get_by_id PASSED                                     [ 70%]
test_todos.py::test_todos_create PASSED                                  [ 72%]
test_todos.py::test_todos_delete PASSED                                  [ 75%]
test_users.py::test_get_user[dict0-1] PASSED                             [ 77%]
test_users.py::test_get_user[dict1-0] PASSED                             [ 80%]
test_users.py::test_get_user[dict2-1] PASSED                             [ 82%]
test_users.py::test_get_user[dict3-1] PASSED                             [ 85%]
test_users.py::test_get_user[dict4-0] FAILED                             [ 87%]
test_users.py::test_status[200-https://jsonplaceholder.typicode.com/users/] PASSED [ 90%]
test_users.py::test_status[404-https://jsonplaceholder.typicode.com/users_no] PASSED [ 92%]
test_users.py::test_get_by_id PASSED                                     [ 95%]
test_users.py::test_users_create PASSED                                  [ 97%]
test_users.py::test_users_delete PASSED                                  [100%]

================================== FAILURES ===================================
______________________________ test_photo_create ______________________________

confserv = <conftest.WORKPLACE object at 0x041F8F10>

    def test_photo_create(confserv):
        with pytest.allure.step("Добавляем фото"):
            create_photo = 'https://jsonplaceholder.typicode.com/photos/'
            status_photo = confserv.jsonplaceholder.photos.create(create_photo, PHOTO_CREATE)
>           assert_that(status_photo, equal_to(STATUS_CREATED), u"Фото не создано")
E           AssertionError: Фото не создано
E           Expected: <201>
E                but: was <500>

test_photos.py:37: AssertionError
___________________________ test_get_user[dict4-0] ____________________________

confserv = <conftest.WORKPLACE object at 0x041F8F10>
dict = {'website': 'elvis.io'}, kol = 0

    @pytest.mark.parametrize("dict, kol", [
        ({'id': 1}, 1),
        ({'id': 1, 'name': 'max'}, 0),
        ({'name': 'Kurtis Weissnat', 'username': 'Elwyn.Skiles'}, 1),
        ({'phone': '(775)976-6794 x41206'}, 1),
        ({'website': 'elvis.io'}, 0)
    ])
    def test_get_user(confserv, dict, kol):
        with pytest.allure.step("Поиск пользателя "):
            url = 'https://jsonplaceholder.typicode.com/users/'
            list = confserv.jsonplaceholder.users.get_users(url, dict)
            print('list =' + str(len(list)))
>           assert_that(len(list), equal_to(kol), u"Кол-во пользователей не совпало")
E           AssertionError: Кол-во пользователей не совпало
E           Expected: <0>
E                but: was <1>

test_users.py:26: AssertionError
---------------------------- Captured stdout call -----------------------------
list =1
==================== 2 failed, 38 passed in 13.57 seconds =====================
