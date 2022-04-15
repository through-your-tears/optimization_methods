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
        let i: number = 0;
        print.push({"id": "1<sup>0</sup>", "ans": `L<sub>0</sub> = [${a}, ${b}], l = ${eps * 2}`});
        let obj: object = find_fib(Math.abs(a - b));
        let n: number = obj.n;
        let F: number = obj.F;
        print.push({"id": "2<sup>0</sup>", "ans": `N = ${n}, F<sub>${n}</sub> = ${F}`});
        print.push({"id": "3<sup>0</sup>", "ans": `k = ${i}`});
        print.push({"id": "3<sup>0</sup>", "ans": `k = ${i}`});
    }
    fibonacci(f, a, b, eps, del);
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}