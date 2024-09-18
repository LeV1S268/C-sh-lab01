Задание 1:
Console.WriteLine("Тип: bool, Минимум = {0}, Максимум = {1}", bool.FalseString, bool.TrueString);
Console.WriteLine("Тип: byte, Минимум = {0}, Максимум = {1}", byte.MinValue, byte.MaxValue);
Console.WriteLine("Тип: sbyte, Минимум: {0}, Максимум: {1}", sbyte.MinValue, sbyte.MaxValue);
Console.WriteLine("Тип: byte, Минимум: {0}, Максимум: {1}", byte.MinValue, byte.MaxValue);
Console.WriteLine("Тип: short, Минимум: {0}, Максимум: {1}", short.MinValue, short.MaxValue);
Console.WriteLine("Тип: ushort, Минимум: {0}, Максимум: {1}", ushort.MinValue, ushort.MaxValue);
Console.WriteLine("Тип: int, Минимум: {0}, Максимум: {1}", int.MinValue, int.MaxValue);
Console.WriteLine("Тип: uint, Минимум: {0}, Максимум: {1}", uint.MinValue, uint.MaxValue);
Console.WriteLine("Тип: long, Минимум: {0}, Максимум: {1}", long.MinValue, long.MaxValue);
Console.WriteLine("Тип: ulong, Минимум: {0}, Максимум: {1}", ulong.MinValue, ulong.MaxValue);
Console.WriteLine("Тип: float, Минимум: {0}, Максимум: {1}", float.MinValue, float.MaxValue);
Console.WriteLine("Тип: double, Минимум: {0}, Максимум: {1}", double.MinValue, double.MaxValue);
Console.WriteLine("Тип: decimal, Минимум: {0}, Максимум: {1}", decimal.MinValue, decimal.MaxValue);
Console.WriteLine("Тип: char, Минимум: {0}, Максимум: {1}", (ushort)char.MinValue, (ushort)char.MaxValue);

Задание 2:
using System.Diagnostics;

Rectangle rectangle = new Rectangle(5, 6);

Console.WriteLine($"Площадь прямоугольника: {rectangle.Area}");
Console.WriteLine($"Периметр прямоугольника: {rectangle.Perimeter}");

Debug.Assert(rectangle.Area == 30);
Console.WriteLine("Тест 1 выполнен");
Debug.Assert(rectangle.Perimeter == 22);
Console.WriteLine("Тест 2 выполнен");
class Rectangle
{
    public double sideA;
    public double sideB;
    public Rectangle(double sideA, double sideB)
    {
        this.sideA = sideA;
        this.sideB = sideB;
    }
    private double CalculateArea()
    {
        return sideA * sideB;
    }
    private double CalculatePerimeter()
    {
        return 2 * (sideA + sideB);
    }
    public double Area
    {
        get { return CalculateArea(); }
    }
    public double Perimeter
    {
        get { return CalculatePerimeter(); }
    }
};

Задание 3:
using System.Diagnostics;

Point p1 = new Point(2, 2);
Point p2 = new Point(2, 6);
Point p3 = new Point(5, 8);
Point p4 = new Point(0, 5);
Point p5 = new Point(7, 0);

Figure triangle = new Figure("Треугольник", p1, p2, p3);

Debug.Assert(triangle.Name == "Треугольник");
Debug.Assert(triangle.PerimeterCalculator() == 14.313755207963359);

Console.WriteLine($"{triangle.Name} c периметром: {triangle.PerimeterCalculator()}");

Figure quadrate = new Figure("Четрырехугольник", p1, p2, p3, p4);

Debug.Assert(quadrate.Name == "Четрырехугольник");
Debug.Assert(quadrate.PerimeterCalculator() == 17.042054445773278);

Console.WriteLine($"{quadrate.Name} с периметром: {quadrate.PerimeterCalculator()}");

Figure pentagon = new Figure("Пятиугольник", p1, p2, p3, p4, p5);

Debug.Assert(pentagon.Name == "Пятиугольник");
Debug.Assert(pentagon.PerimeterCalculator() == 27.42399324448642);

Console.WriteLine($"{pentagon.Name} с периметром {pentagon.PerimeterCalculator()}");


class Point
{
    private int x;
    private int y;
    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
    public int X
    {
        get { return x; }
    }
    public int Y
    {
        get { return y; }
    }
}

class Figure
{
    private Point[] points;
    public string Name { get; set; }
    public Figure(string name, Point p1, Point p2, Point p3)
    {
        Name = name;
        points = new Point[3] { p1, p2, p3 };
    }
    public Figure(string name, Point p1, Point p2, Point p3, Point p4)
    : this(name, p1, p2, p3)
    {
        Array.Resize(ref points, 4);
        points[3] = p4;
    }
    public Figure(string name, Point p1, Point p2, Point p3, Point p4, Point p5)
    : this(name, p1, p2, p3, p4)
    {
        Array.Resize(ref points, 5);
        points[4] = p5;
    }
    public double LengthSide(Point A, Point B)
    {
        return Math.Sqrt(Math.Pow(B.X - A.X, 2) + Math.Pow(B.Y - A.Y, 2));
    }
    public double PerimeterCalculator()
    {
        double perimeter = 0;
        for (int i = 0; i < points.Length; i++)
        {
            Point current = points[i];
            Point next = points[(i + 1) % points.Length];
            perimeter += LengthSide(current, next);
        }
        return perimeter;
    }
}
