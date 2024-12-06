---
hide:
  - toc
---

# Library

=== "C#"

    ```csharp
    namespace AdventOfCode.Lib;

    public sealed record AocInput(
        string Text, 
        IEnumerable<string> Lines, 
        string[] AllLines
    );

    public readonly record struct Point(int X, int Y)
        : IAdditionOperators<Point, Point, Point>, IMultiplyOperators<Point, Point, Point>,
            IMultiplyOperators<Point, int, Point>
    {
        public static readonly Point North = new(0, -1); // Move up
        public static readonly Point NorthEast = new(1, -1); // Move diagonally up-right
        public static readonly Point East = new(1, 0); // Move right
        public static readonly Point SouthEast = new(1, 1); // Move diagonally down-right
        public static readonly Point South = new(0, 1); // Move down
        public static readonly Point SouthWest = new(-1, 1); // Move diagonally down-left
        public static readonly Point West = new(-1, 0); // Move left
        public static readonly Point NorthWest = new(-1, -1); // Move diagonally up-left

        private static readonly Point RotationClockwise90 = new(0, 1);
        
        public static Point operator +(Point p1, Point p2) => new(p1.X + p2.X, p1.Y + p2.Y);
        public static Point operator *(Point p1, Point p2) => new(p1.X * p2.X - p1.Y * p2.Y, p1.X * p2.Y + p1.Y * p2.X);
        public static Point operator *(Point p, int factor) => new(p.X * factor, p.Y * factor);
        
        public static Point RotateRight(Point p) => p * RotationClockwise90; // new(-Y, X)
    }

    public static class FunctionalExtensions
    {
        public static TOut Pipe<TIn, TOut>(this TIn source, Func<TIn, TOut> func) => func(source);
    }
    ```

=== "F#"

    ```fsharp
    
    module Lib =

        [<Struct>]
        type Point = {
            X: int
            Y: int
        } with

            static member North = { X = 0; Y = -1 }
            static member NorthEast = { X = 1; Y = -1 }
            static member East = { X = 1; Y = 0 }
            static member SouthEast = { X = 1; Y = 1 }
            static member South = { X = 0; Y = 1 }
            static member SouthWest = { X = -1; Y = 1 }
            static member West = { X = -1; Y = 0 }
            static member NorthWest = { X = -1; Y = -1 }
            static member RotationClockwise90 = { X = 0; Y = 1 }
            static member (+)(p1: Point, p2: Point) = { X = p1.X + p2.X; Y = p1.Y + p2.Y }

            static member (*)(p1: Point, p2: Point) = {
                X = p1.X * p2.X - p1.Y * p2.Y
                Y = p1.X * p2.Y + p1.Y * p2.X
            }

            static member (*)(p: Point, factor: int) = { X = p.X * factor; Y = p.Y * factor }
            static member rotateRight(p: Point) = p * Point.RotationClockwise90 
    ```
    

=== "Python"

    ```py
    @dataclass(frozen=True)
    class AocInput:
        text: str
        lines: list[str]

    @dataclass(frozen=True, slots=True)
    class Point:
        x: int
        y: int

        def __iter__(self):
            return iter(astuple(self))

        @staticmethod
        def North():
            return Point(0, -1)

        @staticmethod
        def NorthEast():
            return Point(1, -1)

        @staticmethod
        def East():
            return Point(1, 0)

        @staticmethod
        def SouthEast():
            return Point(1, 1)

        @staticmethod
        def South():
            return Point(0, 1)

        @staticmethod
        def SouthWest():
            return Point(-1, 1)

        @staticmethod
        def West():
            return Point(-1, 0)

        @staticmethod
        def NorthWest():
            return Point(-1, -1)

        def __add__(self, point: "Point") -> "Point":
            if isinstance(point, Point) is False:
                return NotImplemented
            return Point(self.x + point.x, self.y + point.y)

        def __mul__(self, factor: int) -> "Point":
            if isinstance(factor, int) is False:
                return NotImplemented
            return Point(self.x * factor, self.y * factor)
    ```