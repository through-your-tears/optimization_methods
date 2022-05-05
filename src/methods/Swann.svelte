<script lang="ts">
    function f(x: number): number {
        return x * x - 4 * x + 7;
    }
    function random (min: number, max: number): number {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    let print: object[] = [];
    function swann(fun: (x: number) => number, eps: number): any {
        let x: number = random(-100, 100);
        let i: number = 0;
        let f0: number = f(x - eps);
        let f1: number = f(x);
        let f2: number = f(x + eps);
        if(f0 >= f1 && f1 <= f2) {
            return [x-eps, x+eps];
        } else while(f0 >= f1 && f1 <= f2 && i < 1000) {
            let x: number = random(-100, 100);
            f0 = f(x - eps);
            f1 = f(x);
            f2 = f(x + eps);
            i++;
        }
        if (i == 1000) {
            return "Функция не является унимодальной";
        } else {
            let a: number;
            let b: number;
            let delta: number;
            let k: number = 1;
            if(f0 >= f1 && f1 >= f2) {
                delta = eps;
                a = x;
                x += eps;
            }
            else {
                delta = eps * -1;
                b = x;
                x -= eps;
            }
            let xk = x + Math.pow(2, k) * delta;
            while (f(xk) < f(x)) {
                if (delta == eps) {
                    a = x;
                }
                else {
                    b = x;
                }
                x = xk;
                xk = x + Math.pow(2, k) * delta;
                k++;
            }
            if (delta == eps) {
                b = xk;
            }
            else {
                a = xk;
            }
            return [a, b];
        }
    }
    let ans: number[] = swann(f, 0.5);
</script>

<!--{#each print as p}-->
<!--    <h3>Шаг {@html p.id}</h3>-->
<!--    <p>{@html p.ans}</p>-->
<!--{/each}-->
<h3>Ответ: a,b = {ans}</h3>