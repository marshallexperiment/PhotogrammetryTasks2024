В этом репозитории предложены задания курса по Фотограмметрии для студентов МКН/ИТМО/ВШЭ.

In this repository, the course assignments for Photogrammetry are offered for students of MKN/ITMO/HSE.

[Остальные задания](https://github.com/PhotogrammetryCourse/PhotogrammetryTasks2024/).

[Other assignments](https://github.com/PhotogrammetryCourse/PhotogrammetryTasks2024/).

# Задание 1. Локальные ключевые точки SIFT (детектор и дескриптор)

# Assignment 1. Local SIFT keypoints (detector and descriptor)

[![Build Status](https://github.com/PhotogrammetryCourse/PhotogrammetryTasks2024/actions/workflows/cmake.yml/badge.svg?branch=task01&event=push)](https://github.com/PhotogrammetryCourse/PhotogrammetryTasks2024/actions/workflows/cmake.yml)

0. Сделать fork проекта (обратите внимание что задание не в ветке **master**, а в ветке **task01**)

0. Fork the project (note that the assignment is not in the **master** branch, but in the **task01** branch)

1. [Установите OpenCV 4.5.1](https://github.com/PhotogrammetryCourse/PhotogrammetryTasks2024/blob/task01/CMakeLists.txt#L19-L31)

1. [Install OpenCV 4.5.1](https://github.com/marshallexperiment/PhotogrammetryTasks2024/blob/Tugas-1/CMakeLists.txt)

2. Выполнить задания ниже (при тестировании Github Actions CI использует GCC 11, поэтому если вы используете фичи свежее чем C++17 - есть риск что не скомпилируется, в таком случае поправьте пожалуйста)

2. Complete the tasks below (during testing, GitHub Actions CI uses GCC 11, so if you are using features newer than C++17, there is a risk it won't compile, in which case please make adjustments)

3. Отправить **Pull-request** с названием```Task01 <Имя> <Фамилия> <Аффиляция>```:

3. Submit a **Pull-request** titled ```Task01 <First Name> <Last Name> <Affiliation>```:

 - Скопируйте в описание [шаблон](https://raw.githubusercontent.com/PhotogrammetryCourse/PhotogrammetryTasks2024/task01/.github/pull_request_template.md)

 - Copy the [template](https://raw.githubusercontent.com/PhotogrammetryCourse/PhotogrammetryTasks2024/task01/.github/pull_request_template.md) into the description

 - Обязательно отправляйте PR из вашей ветки **task01** (вашего форка) в ветку **task01** (основного репозитория)

 - Be sure to submit the PR from your **task01** branch (from your fork) to the **task01** branch (of the main repository)

 - Перечислите свои мысли по вопросам поднятым в коде и просто появившиеся в процессе выполнения задания (выписывайте их с самого начала в отдельный текстовый файл, в шаблоне предложены некоторые вопросы)

 - List your thoughts on the questions raised in the code and those that arose during the assignment (note them from the start in a separate text file; some questions are suggested in the template)

 - Создайте PR

 - Create the PR

 - Затем дождавшись отработку Github Actions CI (около 15 минут) - скопируйте в описание PR вывод исполнения вашей программы **на CI** (через редактирование описания PR)

 - Then, after waiting for GitHub Actions CI to complete (about 15 minutes), copy the output of your program's execution **on CI** into the PR description (by editing the PR description)

**Мягкий дедлайн**: начало лекции 19 февраля. Мягкий дедлайн - ориентировочная рекомендация "здорово если успеете".

**Soft deadline**: the beginning of the lecture on February 19. The soft deadline is a tentative recommendation: "It's great if you make it."

**Жесткий дедлайн**: начало лекции 26 февраля. Жесткий дедлайн - предполагается что все в него укладываются. Не доделали - зашлите хотя бы что-то. После дедлайна досылать тоже можно (но будет небольшой штраф в баллах).

**Hard deadline**: the beginning of the lecture on February 26. The hard deadline is expected to be met by everyone. If you haven't finished, send whatever you have. Submissions after the deadline are also allowed (but there will be a small penalty in points).

Задание 1.0.
=========

Assignment 1.0.
=========

Ознакомьтесь со структурой проекта:

Familiarize yourself with the project structure:

1. ```src/phg/sift/``` - основная часть где вы будете реализовывать алгоритм

1. ```src/phg/sift/``` - the main part where you will implement the algorithm

2. ```tests/test_sift.cpp``` - тесты которые будут прогонять ваш алгоритм на каких-то относительно простых манипуляциях с маленькой картинкой, если вам хочется добавить другие сценарии тестирования (возможно с другими метриками) - здорово!

2. ```tests/test_sift.cpp``` - tests that will run your algorithm on some relatively simple manipulations with a small image; if you want to add other testing scenarios (possibly with different metrics) - that's great!

3. ```data/src``` - исходные данные используемые при тестировании (к ним используются относительные пути, поэтому нужно выставить Working directory = путь к проекту)

3. ```data/src``` - source data used during testing (relative paths are used, so you need to set the Working directory = project path)

4. ```data/debug/test_sift/SIFT``` - сюда тесты сохранят картинки с визуализацией результата

4. ```data/debug/test_sift/SIFT``` - this is where tests will save images with the result visualization

5. ```data/debug/test_sift/debug``` - сюда вам предлагается сохранять любые промежуточные картинки-визуализации, это очень полезно для отладки, оценки качества, уверенности и в целом один из немногих способов качественно "заглянуть в черную коробку"

5. ```data/debug/test_sift/debug``` - this is where you are encouraged to save any intermediate visualization images; this is very useful for debugging, quality assessment, confidence, and overall one of the few ways to effectively "look inside the black box"

Задание 1.1.
=========

Assignment 1.1.
=========

1. Убедитесь что у вас все компилируется и тесты проходят.

1. Make sure everything compiles and tests pass.

2. Ознакомьтесь с тем как проводится тестирование - ```tests/test_sift.cpp```:

2. Familiarize yourself with how the testing is conducted - ```tests/test_sift.cpp```:

3. Обратите внимание что там сравнивается ORB и SIFT реализованные в OpenCV

3. Note that ORB and SIFT implemented in OpenCV are compared there

4. Посмотрите и сравните результаты этих двух дескрипторов:

4. Look at and compare the results of these two descriptors:

 - по логам в т.ч. пишущим угол поворота, перепад масштаба и расстояние между дескрипторами)

 - by logs, including those that write the rotation angle, scale change, and distance between descriptors)

 - по картинкам с результатами в папке ```data/debug/test_sift/SIFT```

 - by images with results in the folder ```data/debug/test_sift/SIFT```

Задание 1.2.
=========

Assignment 1.2.
=========

Включите тестирование вашего SIFT - см. **TODO** в ```test/test_sift.cpp```

Enable testing of your SIFT - see **TODO** in ```test/test_sift.cpp```

Реализуйте SIFT в ```src/phg/sift/sift.cpp```:

Implement SIFT in ```src/phg/sift/sift.cpp```:

 - Либо с чистого листа самостоятельно - просто удалите оттуда весь код (тогда если все хорошо - **10 баллов**)

 - Either from scratch on your own - just delete all the code from there (then if everything is good - **10 points**)

 - Либо выполняя **TODO** один за другим (через Ctrl+F сверху вниз) (тогда если все хорошо - **8 баллов**)

 - Or by completing **TODO** one by one (through Ctrl+F from top to bottom) (then if everything is good - **8 points**)

 - Либо выполняя **TODO** один за другим, а если на каких-то отдельных этапах вы хотите сделать больше самостоятельно - смело удаляйте окружающий код заготовки :) (тоже если все хорошо - **8 баллов**)

 - Or by completing **TODO** one by one, and if at some stages you want to do more independently - feel free to delete the surrounding boilerplate code :) (also if everything is good - **8 points**)
