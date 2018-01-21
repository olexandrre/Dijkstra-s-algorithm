#include <iostream>
#include <vector>
#include <stdio.h>
#include <SFML/Graphics.hpp>
#include <string>
#include <stdlib.h>
#include <sstream>
#include <math.h>
using namespace std;

vector< vector<int> > read (int n)
{
    setlocale(LC_ALL,"RUS");
    vector< vector<int> > basic (n);/// Вводная табличка
    int value;
    bool check = 0;
    do {
        check = 0;
        for (int i = 0; i < basic.size(); i++)
        {
            for (int j = 0; j < n; j++)
            {
                cin >> value;
                basic[i].push_back(value);
            }
        }
        for (int i = 0; i < n; i++)
            if (basic[i][i] != 0)
                check = 1;
        if (check == 1)
            cout << "Неправильный ввод данных";
    } while(check == 1);
    cout << endl;
    cout << "Откуда?" << endl;
    cin >> value;
    basic[n - 1].push_back(value);
    do {
        check = 0;
        cout << "Куда?" << endl;
        cin >> value;
        if (value == basic[n - 1][n])
        {
            check = 1;
            cout << "Перестань играться" << endl;
        }
    } while (check == 1);
    basic[n - 1].push_back(value);
    return basic;
}
vector <int> short_way (int n, vector< vector <int> >basic)
{
    int begin ,end;
    begin = basic[n - 1][n];
    end = basic[n - 1][n + 1];
    vector <int> result;
    int **a = new int *[n + 1];/// Табличка, в которой всё считается
    int *p = new int [n];///                                                                 Вершина(i):
/// Предыдущая вершина от данной вершины (i), лежащая на кратчайшем пути от начала до данной вершины(i):
    vector <int> visitors; /// Вершины ,которые мы уже посетили (т.е учли все пути ,отходящие от вершин в visitors)
    vector <pair <int,int>> choose;/// c помощью него находим вершину ,которая не в visitors ,и от начала до неё наиболее кратчайший путь
    for (int i = 0; i < n + 1; i++)
    {
        a[i] = new int [n - 1];
    }
    int temp = 0;
    for (int j = 0; j < n - 1 ;j++) /// Заполняем верхушку на массиве a;
    {
        if (temp != begin)
            a[0][j] = temp ;
        else
        {
            temp++;
            a[0][j] = temp;
        }
        temp++;
    }
    temp = begin;
    for (int i = 1; i < n + 1; i++)
    {
        visitors.push_back(temp);
        for (int j = 0; j < n - 1; j++)
        {
            if (i == 1)
            {
                if (basic[visitors[i - 1]][a[0][j]] == 0)
                    a[i][j] = INT_MAX;
                else {
                        a[i][j] = basic[visitors[i - 1]][a[0][j]];
                        p[a[0][j]] = visitors[i - 1];
                    }
            } else
            {
                if (basic[visitors[i - 1]][a[0][j]] == 0)
                    a[i][j] = a[i-1][j];
                else
                {
                    if (visitors[i - 1] < begin)
                    {
                        if (basic[visitors[i - 1]][a[0][j]] + a[i - 1][visitors[i - 1]] < a[i - 1][j])
                        {
                            a[i][j] = basic[visitors[i - 1]][a[0][j]] + a[i - 1][visitors[i - 1]];
                            p[a[0][j]] = visitors[i - 1];
                        } else
                            a[i][j] = a[i - 1][j];
                    }else
                    {
                        if (basic[visitors[i - 1]][a[0][j]] + a[i - 1][visitors[i - 1] - 1] < a[i - 1][j])
                        {
                            a[i][j] = basic[visitors[i - 1]][a[0][j]] + a[i - 1][visitors[i - 1] - 1];
                            p[a[0][j]] = visitors[i - 1];;
                        }
                        else
                            a[i][j] = a[i - 1][j];
                    }
                }
            }
        }
        int check = 1;
        for (int j = 0; j < n - 1; j++)
        {
            choose.push_back(make_pair(a[0][j], a[i][j]));
        }
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = i - 1; j >= 0; j--)
            {
                if (choose[j].second > choose[j + 1].second)
                    swap(choose[j],choose[j + 1]);
            }
        }
        int j = 0;
        for (; check != 0; j++)
        {
            check = 0;
            for (int i = 0; i < visitors.size(); i++)
            {
                if (choose[j].first == visitors[i])
                    check = 1;
            }
        }
        j--;
        temp = choose[j].first;
        choose.clear();
    }
    result.push_back(end);
    int prev = end;
    while (prev != begin)
    {
        result.insert(result.begin(), p[prev]);
        prev = p[prev];
    }
    return result;
}
    template <typename T>
    std::string toString(T val)
    {
        std::ostringstream oss;
        oss<< val;
        return oss.str();
    }
    void Picture(int n ,vector <int> result, vector< vector<int> > basic)
    {
        vector < pair<double, double>> position (n);
        sf::RenderWindow window(sf::VideoMode(1360, 720), "SFML works!");
        sf::CircleShape circle(12);
        circle.setFillColor(sf::Color::Green);
        double angel;
        angel = 6.28/ n;
        double tempangel = 0;
        sf::Font font;
        font.loadFromFile("times-new-roman.ttf");
        sf::Text text("", font, 15);
        text.setColor(sf::Color::Red);
        text.setStyle(sf::Text::Bold);
        window.isOpen();
        for (int i = 0; i < n; i++)
        {
            double tempsin, tempcos;
            if (tempangel <= 1.57){
                tempsin = sin(tempangel);
                tempcos = -cos(tempangel);
            } else if (tempangel <= 3.14)
            {
                tempsin = sin(3.14 - tempangel);
                tempcos = cos(3.14 - tempangel);
            } else if (tempangel <= 4,71){
                tempsin = -sin(tempangel - 3.14);
                tempcos = cos(tempangel - 3.14);
            } else if (tempangel < 6.28){
                tempsin = -sin(6.28 - tempangel);
                tempcos = -cos(6.28 - tempangel);
            }
            position[i].first = 500 + 330 * tempsin;
            position[i].second = 350 + 330 * tempcos;
            text.setPosition(501 + 352.5 * tempsin, 350 + 350 * tempcos);
            std::string str;
            str = toString<double>(i);
            text.setString(str);
            window.draw(text);
            tempangel += angel;
        }
        int count_ = 0;
        for (int i = 0; i < n; i++){
            for (int j = 0; j < n; j++){
                if (basic[i][j] != 0)
                    count_++;
            }
        }
        sf::VertexArray lines(sf::Lines, 4 * count_);
        int index  = 0;
        int check_ = 0;
        for (int i = 0; i < n; i++){
            check_ = -1;
            for (int l = 0; l < result.size() - 1; l++)
                    if (result[l] == i)
                        check_ = l + 1;
            for (int j = 0; j < n; j++){
                if (basic[i][j] != 0)
                {
                    lines[index].position = sf::Vector2f(position[i].first + 12, position[i].second + 12);
                    lines[index + 1].position = sf::Vector2f(position[j].first + 12, position[j].second + 12);
                    if (check_ != -1 && result[check_] == j)
                    {
                        lines[index].color= sf::Color::Red;
                        lines[index + 1].color= sf::Color::Red;
                    } else {
                        lines[index].color= sf::Color::White;
                        lines[index + 1].color= sf::Color::White;
                    }
                    index += 2;
                }
            }
        }
        window.draw(lines);
        int step = 0;
        for (int i = 0 ; i < n; i++)
        {
            if (i == result[step])
            {
                circle.setFillColor(sf::Color::Red);
                step++;
            }
            circle.setPosition(position[i].first, position[i].second);
            window.draw(circle);
            circle.setFillColor(sf::Color::Green);
        }
        sf::CircleShape circle1(5, 3);
        circle1.setFillColor(sf::Color::Blue);
        float distance;
        check_ = 0;
        for (int i = 0; i < n; i++){
                check_ = 0;
                for (int l = 0; l < result.size() - 1; l++)
                    if (result[l] == i)
                            check_ = l + 1;
                for (int j = 0; j < n; j++){
                    if (basic[i][j] != 0){
                        distance = sqrt((position[i].first - position[j].first) * (position[i].first - position[j].first) + (position[i].second - position[j].second)* (position[i].second - position[j].second));
                        circle1.setPosition(12 + position[j].first + (((position[i].first - position[j].first)* 12)/distance) - 5,position[j].second + 12 + (((position[i].second - position[j].second)* 12)/distance) - 5);
                        if (check_ != 0 && result[check_] == j)
                        {
                                  circle1.setFillColor(sf::Color::Magenta);
                        }
                        window.draw(circle1);
                        circle1.setFillColor(sf::Color::Blue);
                    }
                }
        }
        window.display();
        int check = 0;
        while(check != 1){
            sf::Event event;
            while (window.pollEvent(event))
                if (event.type == sf::Event::Closed){
                        window.close();
                        check = 1;
                }
        }
}
int main()
{
    vector< vector<int> > basic; /// Ввод
    vector <int> result; /// Кратчайший путь
    int n; /// Кол -во вершин
    cin >> n;
    basic = read(n);
    result = short_way(n, basic);
    Picture(n, result, basic);
    /// Красный цвет круга и линии ,значит они задействованы в кратчайшем пути
    /// Зелёный цыет круга и белый линии не задействованы
    /// Синий треугольничек -не задействован
    /// Фиолетовый треугольник - задействован
    return 0;
}
