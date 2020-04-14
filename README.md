# WindowsApplication
### Задание реализовать анимацю "стрелочки часиков"

Сделай fork проекта и измени функцию отрисовки LRESULT CALLBACK WndProc

##### 1 шаг
Удали все внутрености оставив функцию такого вида.   
и в начале проекта добавьте математическую библиотеку #include <math.h> (для использования функций sin и cos)●●
LRESULT CALLBACK WndProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam). 
{ 
///тут пусто
  return 0;     
}


##### 2 шаг
Добавьте следующие параметры 
///тип PAINTSTRUCT - это структура для окрашивния рабочей области
///тип HDC - устройство отображения, который используют чтобы красить
///тип POINT - структура описывающая текущее положение пера(точку)
    PAINTSTRUCT ps;
    HDC hdc;
    POINT p;
После опишите на переменные point'ов 
  static float x=300 , y=400 , r=100;
  static double i;
  static int x0 = 400, y0 = 400;
  
##### 3 шаг
После добавьте выборку обработок сообщений
switch - это аналог if else. Внутри скобок описывается переменная - затем через консутркцию описывается чему переменная равна.
И если условие верно, то выполняется действие. Если ни одно условие не удовлетворяет то выполняется по умоляанию default
switch (message)
    {
    ///тут добавтье 4 шаг
    default: return DefWindowProc(hWnd, message, wParam, lParam);
    }
DefWindowProc - обработчик любого окна

##### 4 шаг
Теперь ВНУТРЬ конструкции switch (message) добавьте системные команды

case WM_CREATE:
    SetTimer(hWnd, 1, 1000, NULL);//создает таймер с указанным интервалом 
    break;
case WM_TIMER:
    i+=0.2;
    y = sin(i)*r;
    x = cos(i)*r;
    y += y0; x += x0;
    InvalidateRect(hWnd, NULL, TRUE);//отрисовывает прямоугольник
    break;
case WM_PAINT:
    hdc = BeginPaint(hWnd, &ps);//назначения отрисовки для главного окна
    MoveToEx(hdc, x0, y0, &p);// перемещение пера для отрисовки
    LineTo(hdc, x, y);//отрисовка линии по таймкоду
    EndPaint(hWnd, &ps);
    break;
case WM_DESTROY:
    KillTimer(hWnd, 1);//уничтожение предыдущей линии
    PostQuitMessage(0);
    break;
    
### ЕСЛИ все шаги выполнены то ошибок не будет :)
