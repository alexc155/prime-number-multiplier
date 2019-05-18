# prime-number-multiplier

My quick version of the prime number multiplier task for interviewees:

```c#
using System;
using System.Collections.Generic;
using System.Diagnostics;

namespace Prime_Numbers
{
    public class Program
    {
        public static void Main(string[] args)
        {
            Console.Write("Enter a max number:");
            var input = Console.ReadLine();
            var limit = uint.Parse(input);
            Console.WriteLine("\n");

            var s = new Stopwatch();
            s.Start();

            var isPrime = true;
            var primes = new List<uint>(int.Parse(input) / 2) {2};
			
            Console.Write("\t2");

            for (uint i = 3; i <= limit; i+=2)
            {
                isPrime = true;
                uint upperLimit = (uint)(Math.Sqrt(i));

                foreach (uint prime in primes)
                {
                    if (prime > upperLimit)
                        break;

                    if (i % prime == 0)
                    {
                        isPrime = false;
                        break;
                    }
                }
                if (isPrime)
                {
                    Console.Write("\t" + i);
                    primes.Add(i);
                }
            }

            Console.WriteLine("\n");

            foreach (var prime in primes)
            {
                Console.Write(prime + "\t");
                foreach (var mult in primes)
                {
                    Console.Write(prime * mult + "\t");
                }
                Console.Write("\n");
            }

            s.Stop();
            Console.WriteLine("\nTime: " + s.ElapsedMilliseconds / 1000.0);
        }
    }
}
```

[Run it here](https://dotnetfiddle.net/Ci0LRY) When n = 500, time taken = 0.003s

Another version

```c#
using System;
using System.Collections.Generic;
using System.Diagnostics;

namespace Prime_Numbers
{
    public static class Program
    {
        public static bool[] nonprimes;
        public static uint i = 2;
        public static uint inputnumber;

        public static void Main(string[] args)
        {
            Console.Write("Enter a max number:");
            var inputvar = Console.ReadLine();

            var s = Stopwatch.StartNew();

            inputnumber = Convert.ToUInt32(inputvar);
            nonprimes = new bool[inputnumber + 1];

            nonprimes[0] = true;
            nonprimes[1] = true;

            calcprime();
            i++;

            while (i < inputnumber)
            {
                calcprime();
                i += 2;
            }

            var primes = new List<uint>(1000000);
            uint counter = 0;
            foreach (var element in nonprimes)
            {
                if (!element)
                {
                    primes.Add(counter);
                    Console.Write("\t" + counter);
                }
                counter++;
            }

            Console.Write("\n");

            foreach (var prime in primes)
            {
                Console.Write(prime + "\t");
                foreach (var mult in primes)
                {
                    Console.Write(prime * mult + "\t");
                }
                Console.Write("\n");
            }

            s.Stop();
            Console.WriteLine("\nTime: " + s.ElapsedMilliseconds / 1000.0);

        }

        public static void calcprime()
        {
            uint k = 2;
            var j = i;
            while (j * k <= inputnumber)
            {
                nonprimes[j * k] = true;
                k++;
            }
        }
    }
}
```

[Run it here](https://dotnetfiddle.net/FrRb5w) When n = 500, time taken = 0.003s
