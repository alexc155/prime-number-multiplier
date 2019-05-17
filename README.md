# prime-number-multiplier

My quick version of the prime number multiplier task for interviewees:

```c#
using System;
using System.Collections.Generic;
using System.Diagnostics;

namespace Prime_Numbers
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter a max number:");
            var limit = int.Parse(Console.ReadLine());
            Console.WriteLine("\n");

            var s = new Stopwatch();
            s.Start();

            var isPrime = true;
            var primes = new List<int>();
            for (var i = 2; i <= limit; i++)
            {
                for (var j = 2; j <= limit; j++)
                {
                    if (i == j || i % j != 0) continue;
                    isPrime = false;
                    break;
                }
                if (isPrime)
                {
                    Console.Write("\t" + i);
                    primes.Add(i);
                }
                isPrime = true;
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
            Console.ReadKey();
        }
    }
}
```

[Run it here](https://dotnetfiddle.net/Ci0LRY) When n = 400, time taken = 0.015s
