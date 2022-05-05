<script lang="ts">
    function find_fib(x: number): object {
        let i: number = 2;
        let a: number = 1;
        let b: number = 1;
        while (a + b < x) {
            let p: number = a;
            a = b;
            b += p;
            i++;
        }
        return {"n": i, "F": a + b};
    }
    function fib(n: number) {
        if(n == 1 || n == 0) {
            return 1;
        }
        return fib(n-1) + fib(n-2);
    }
    function f(x: number): number {
        return x * x - 4 * x + 7;
    }
    const a = 0;
    const b = 10;
    const eps: number = 0.5;
    const del: number = 0.2;
    let print: object[] = [];
    let pred_pogr: number = 0;
    function fibonacci(fun: (x: number) => number, a: number, b: number, eps: number, delta: number) {
        let k: number = 0;
        print.push({"id": "1<sup>0</sup>", "ans": `L<sub>0</sub> = [${a}, ${b}], l = ${eps * 2}`});
        let obj: object = find_fib(b - a);
        let n: number = obj.n;
        let F: number = obj.F;
        print.push({"id": "2<sup>0</sup>", "ans": `N = ${n}, F<sub>${n}</sub> = ${F}`});
        print.push({"id": "3<sup>0</sup>", "ans": `k = ${k}`});
        let y: number = a + fib(n - 2) * (b - a) / fib(n);
        let z: number = a + fib(n - 1) * (b - a) / fib(n);
        print.push({"id": "4<sup>0</sup>", "ans": `y<sub>0</sub> = a<sub>0</sub> + F<sub>N-2</sub> / F<sub>N</sub> * (b<sub>0</sub> - a<sub>0</sub>) = ${y}, z<sub>0</sub> = a<sub>0</sub> + F<sub>N-1</sub> / F<sub>N</sub> * (b<sub>0</sub> - a<sub>0</sub>) = ${z} `});
        do {
            print.push({"id": `5<sup>${k}</sup>`, "ans": `f(y<sub>${k}</sub>) = ${f(y)}, f(z<sub>${k}</sub>) = ${f(z)}`});
            if(f(y) <= f(z)) {
                b = z;
                z = y;
                y = a + fib(n - k - 3) / fib(n - k - 1) * (b - a);
            }
            else {
                a = y;
                y = z;
                z = a + fib(n - k - 2) / fib(n - k - 1) * (b - a);
            }
            print.push({"id": `6<sup>${k}</sup>`, "ans": `a<sub>${k+1}</sub> = ${a}, b<sub>${k+1}</sub> = ${b}, y<sub>${k+1}</sub> = ${y}, z<sub>${k+1}</sub> = ${z}`});
            print.push({"id": `7<sup>${k}</sup>`, "ans": `N - 3 = ${n-3}, k = ${k}, L<sub>${k+2} = [${a}, ${b}]`});
            k++;
        } while (k <= n - 3)
        y = (a + b) / 2;
        z = y + delta;
        if(f(y) > f(z)) {
            a = y;
        }
        else {
            b = z;
        }
        print.pop();
        k--;
        print.push({"id": `7<sup>${k}</sup>`, "ans": `N - 3 = ${n-3}, k = ${k}, L<sub>${k+2} = [${a}, ${b}]`});
        pred_pogr = Math.abs(a - b) / 2;
        return (a + b) / 2;
    }
    // переделай ебучие кривые выводы()
    let ans:number = fibonacci(f, a, b, eps, del);
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}
<h3>Ответ: x = {ans}, предельная погрешность = {pred_pogr}</h3>