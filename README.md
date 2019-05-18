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
            var limit = ulong.Parse(input);
            Console.WriteLine("\n");

            var s = new Stopwatch();
            s.Start();

            var isPrime = true;
            var primes = new List<ulong>(int.Parse(input) / 2) {2};
			
            Console.Write("\t2");

            for (ulong i = 3; i <= limit; i+=2)
            {
                isPrime = true;
                ulong upperLimit = (ulong)(Math.Sqrt(i));

                foreach (ulong prime in primes)
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
