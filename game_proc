#include <iostream>
#include <string>

using namespace std;


// показывает расположение объектов (левый берег  <-река->  правый берег)
void show_place(const int *pos, const string* name, const int LEN) {
    int i = 0;

    // копируем массив что бы изменять в нём параметры
    int* temp = new int [LEN];
    for (int i = 0; i < LEN; i++)
    {
        temp[i] = pos[i];
    }
    
    cout << "левый берег" << "\t\t" << "правый берег" <<
        endl << "************************************" << endl;
    bool check = true;
    while (check) {
        check = false;

        // проверяем есть ли хоть одна переменная с положительным значением
        // если есть, значит не все объекты выведены на экран
        for (int i = 0; i < LEN; i++)
        {
            if (temp[i] >= 0)
            {
                check = true;
                break;
            }
        }


        // дальше разделаем блок выовода на 3 части
        // левый берег | река (тут всегда "\t\t") | правый берег

        if (check) {
            bool var = false;

            // проверяем все объекты с значение 0, если нашли то выводим на экран
            for (int i = 0; i < LEN; i++)
            {
                if (temp[i] == 0) {
                    if (pos[0] == 0)
                        cout << "(" << i << ")";
                    cout << name[i];
                    temp[i] = -1;
                    var = true;
                    break;
                }
            }
            // если не нашли, вставляем на место \t
            if (!var)
                cout << "\t";

            // блок реки
            cout << "\t\t";

            // правый берег
            for (int i = 0; i < LEN; i++)
            {
                if (temp[i] == 1) {
                    if (pos[0] == 1)
                        cout << "(" << i << ")";
                    cout << name[i];
                    temp[i] = -1;
                    break;
                }
            }
            cout << endl;
        }
    }
    delete[] temp;
    temp = nullptr;
}



// тут должна быть история
void intro() {
    cout <<
        "введение:\n" <<
        "бла бла бла\n" <<
        "бла бла бла\n" <<
        "бла бла бла\n" <<
        "бла бла бла\n" <<
        "бла бла бла\n" <<
        "************" << endl << endl;
}


// работа в окне консоли с cin
// проверка вводимых значение в консоль пользователем, доступны только:
// restart, exit, 0, 1, 2, 3
// от 0 до 3 доступны только в том случае, если главный объект(0-Вы) находится в одном диапазоне с выбраным объектом
// если при вызове функции res_exit оставлять дефолтным, то будет выполнятся всё тело функции
// если res_exit=true, то будем ждать только 2 фразы, restart и exit
int get_var(string restart, string exit, bool& game, const int LEN, int* pos, bool res_exit = false) {
    string temp;
    while (true)
    {
        cin >> temp;
        cout << endl;

        try {
            // res_exit = true
            if (restart == temp) {
                return -1;
            }

            if (exit == temp) {
                game = false;
                cout << "Выходим!" << endl;
                return -1;
            }
            if (res_exit) {
                throw exception();
            }

            // res_exit = false (default)
            int t = stoi(temp);
            if (t >= 0 && t < LEN && pos[t] == pos[0]) {
                return stoi(temp);
            }
            throw stoi(temp);
        }
        catch (const exception&) {
            cerr << "Не верная команда: (" << temp << ")! попробуйте ещё раз..." << endl;
        }
        catch (const int) {
            cerr << "Не верное чило: (" << temp << ")! попробуйте ещё раз..." << endl;
        }
    }
}


// изменения параметров объекта в связи с перемещением
void processed_var(int* pos, int var) {
    if (var != 0) {
        if (pos[var] == 0) {
            pos[var]++;
        }
        else
        {
            pos[var]--;
        }
    }

    if (pos[0] == 0) {
        pos[0]++;
    }
    else
    {
        pos[0]--;
    }
}


// проверка результата перемещения и вывод соответствующей реакции на условия
void get_result(int* pos, string* name, const int LEN, int &var, bool& game, string restart, string exit) {
    bool result = true;

    for (int i = 0; i < LEN; i++)
    {
        if (pos[i] == 0)
            break;
        if (i == LEN - 1) {
            cout << "Все переправленны в целости и сохранности! Вы ВЫЙГРАЛИ!" << endl << endl << endl;
            cout << "Начать заного: " << restart << "\nВыйти: " << exit << endl << endl;
            var = get_var(restart, exit, game, LEN, pos, true);
        }
    }

    if (pos[0] != pos[2] && pos[1] == pos[2]) {
        cout << name[1] << " съела " << name[2] << endl;
        result = false;
    }

    if (pos[0] != pos[3] && pos[2] == pos[3]) {
        cout << name[2] << " съела " << name[3] << endl;
        result = false;
    }
    if (!result) {
        cout << "Игра окончена! Вы проиграли :/" << endl << endl << endl;
        cout << "Начать заного: " << restart << "\nВыйти: " << exit << endl << endl;
        var = get_var(restart, exit, game, LEN, pos, true);
    }
    
}


int main()
{
    setlocale(LC_ALL, "ru");

    intro();

    const int LEN = 4;
    int pos[LEN]{ 0,0,0,0 };

    string name[LEN]{ 
        "пастух  ",
        "собака  ",
        "козочка ", 
        "капустка"
    };
    string restart = "restart";
    string exit = "exit";
    bool game = true;
    int var = 0;
    while (game) {
        cout << "Начать заного: " << restart << "\nВыйти: " << exit << endl << endl;
        cout << "Выберите цифру того, кого перевезти или 0 если переплыть одному:" << endl << endl;
        if (var != -1 && game) {
            show_place(pos, name, LEN);
            var = get_var(restart, exit, game, LEN, pos);
        }

        if (var == -1 && game) {
            for (int i = 0; i < LEN; i++)
            {
                pos[i] = 0;
            }
            var = 0;
            system("CLS");
            cout << "Перезагружаем игру!" << endl << endl;
            intro();
            continue;
        }

        processed_var(pos, var);
        get_result(pos, name, LEN, var, game, restart, exit);
    }

    system("pause");
}
