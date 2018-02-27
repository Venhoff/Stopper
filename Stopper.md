# Stopper
Prosty program symulujacy stopper.

        namespace Stopper
        {
            class Program
            {
                static void Main(string[] args)
                {
                    Console.WriteLine("Program Stopper posiada nastepujące komendy:" + "\n" +
                        "1 - rozpoczyna odliczanie. Niemożna dwa razy pod rząd uruchomic stoppera;" + "\n" +
                        "2 - zatrzymuje stopper;" + "\n" +
                        "3 - zamyka program.");
                    Console.WriteLine("Po każdym stopie zostanioe wyśiwtlony przebieg.");

                    Licznik licznik = new Licznik();
                    var input ="";

                    while (input != "3")
                    {
                        Console.WriteLine("Podaj komendę:");
                        input = Convert.ToString(Console.ReadLine());
                        input = input.ToLower();
                        if (input == "1")
                        {
                            licznik.Start();
                            continue;
                        }
                        else if (input == "2")
                        {
                            licznik.Stop();
                            Console.WriteLine("Czas:" + licznik.Przebieg.TotalSeconds + " s");
                            continue;
                        }
                        else if (input == "3")
                            continue;
                        else
                        {
                            Console.WriteLine("Nie poprawane komedna. Spróbuj ponownie.");
                            continue;
                        }
                    }
                }
            }
        }

    public class Licznik
    {
        private static bool _Działa;
        private DateTime _Start { get; set; }
        private DateTime _Stop { get; set; }

        public void Start()
        {
            
            if (_Działa == false)
            {
                _Działa = true;
                _Start = DateTime.Now;
            }
            else
                throw new System.InvalidOperationException("Stopper juz działa.");

        }
        public void Stop()
        {
            
            if (_Działa == true)
            {
                _Działa = false;
                _Stop = DateTime.Now;
            }
            else
                Console.WriteLine("Program jest już zatrzymany.");
        }
        
        public TimeSpan Przebieg
        {
            get
            {
                var czas = _Stop - _Start;
                return czas;
            }
        }
    }
