using System;

namespace Generator
{
	class Program
	{
		public static void Render (int x, int y, int width, int heidht, Point[,] points)
		{
			Console.Clear ();
			//проход по окну консоли для отрисовки кусока карты
			for (int iy = y; iy < heidht + y - 1; iy++){
				for (int ix = x; ix < width + x; ix++) {
					switch (points [ix, iy].Color){
					//определение цвета
					case "blue":
						Console.ForegroundColor = ConsoleColor.Blue;
						break;
					case "brown":
						Console.ForegroundColor = ConsoleColor.DarkYellow;
						break;
					case "green":
						Console.ForegroundColor = ConsoleColor.Green;
						break;
					case "yellow":
						Console.ForegroundColor = ConsoleColor.Yellow;
						break;
					}
					//отрисовка объекта
					Console.Write (points [ix, iy].Type);
				}
			}
		}

		public static void Main (string[] args)
		{
			//задание размера карты
			int width = 500;
			int height = 500;

			//массив типов местности
			Point[,] points = new Point[width, height];
			Random radnom = new Random ();

			Console.Write ("Loading.");
			//генерирование поверхности
			for (int y = 0; y < height; y++){
				for (int x = 0; x < width; x++) {
					int randomType = radnom.Next (0, 4);
					switch (randomType) {
					case 0:
						points [x, y] = new Point ();
						break;
					case 1:
						points [x, y] = new Point (Convert.ToChar (9617), "ground", "brown");
						break;
					case 2:
						points [x, y] = new Point ('^', "wood", "green");
						break;
					case 3:
						points [x, y] = new Point ('~', "desert", "yellow");
						break;
					}
				}
				//периодически выводим точки для показания процесса
				if (y % 100 == 0) {
					Console.Write ('.');
				}
			}
			//определение поциции камеры, а также нажатой клавиши
			int camX = 0;
			int camY = 0;
			System.ConsoleKeyInfo key;

			//основной цыкл
			do {
				Render(camX, camY, Console.WindowWidth, Console.WindowHeight, points);
				
				key = Console.ReadKey ();

				//перемешение камеры
				switch (key.KeyChar) {
				case 'a':
					camX--;
					break;
				case 'w':
					camY--;
					break;
				case 'd':
					camX++;
					break;
				case 's':
					camY++;
					break;
				default:
					//сообщаем кнопки управления
					Console.Write ("use 'wasd' or 'e'");
					break;
				}
				//не пускаем камеру за края карты
				if (camX < 0){
					camX = 0;
				}
				//необычная логика потому что камера находиться в левом верхнем
				//углу экрана, и отрисовка происходит от туда
				else if (camX + Console.WindowWidth > width){
					camX = width - Console.WindowWidth;
				}

				if (camY < 0){
					camY = 0;
				}
				else if (camY + Console.WindowHeight > height){
					camY = height - Console.WindowHeight;
				}
			//завершаем цыкл если нажата 'e'
			} while (key.KeyChar != 'e');
		}
	}
	class Point {
		private char type;
		private string name;
		private string color;

		public Point(){
			//упрощенная реализация воды
			this.type = '~';
			this.name = "water";
			this.color = "blue";
		}
		public Point(char type, string name, string color){
			this.type = type;
			this.name = name;
			this.color = color;
		}
		//установка режима свободного чтения всех переменных
		public char Type
		{ 
			get{
				return type;
			}
		}
		public string Name
		{ 
			get{
				return name;
			}
		}
		public string Color
		{ 
			get{
				return color;
			}
		}
	}
}
