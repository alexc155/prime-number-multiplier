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
        public static void Main(string[] args)
        {
            Console.Write("Enter a max number:");
            string inputvar = Console.ReadLine();

            var s = Stopwatch.StartNew();

            uint inputnumber = Convert.ToUInt32(inputvar);
            bool[] nonprimes = new bool[inputnumber + 1];

            nonprimes[0] = true;
            nonprimes[1] = true;

            for (uint i = 3; i < inputnumber; i += 2)
            {
                uint k = 2;
                uint j = i;
                while (j * k <= inputnumber)
                {
                    nonprimes[j * k] = true;
                    k++;
                }
            }

            var primes = new List<uint>((int)inputnumber / 2);
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
    }
}
```

[Run it here](https://dotnetfiddle.net/FrRb5w) When n = 500, time taken = 0.003s
