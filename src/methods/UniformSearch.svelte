<script lang="ts">
    let print:object[] = [];
    function random (min: number, max: number): number {
        return Math.floor(Math.random() * (max - min + 1)) + min;
    }
    function swann(f: (x: number) => number, eps: number): any {
        let x: number = random(-100, 100);
        let i: number = 0;
        let f0: number = f(x - eps);
        let f1: number = f(x);
        let f2: number = f(x + eps);
        print.push({"id": "1<sup>0</sup>", "ans": `t ${eps}, x = ${x}`})
        print.push({"id": "2<sup>0</sup>", "ans": `f(x - t) = ${f0}, f(x) = ${f0}, f(x + t) = ${f2}`})
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
                print.push({"id": "4<sup>0</sup>", "ans": `delta = ${delta}, a = ${a}`})
            }
            else {
                delta = eps * -1;
                b = x;
                x -= eps;
                print.push({"id": "4<sup>0</sup>", "ans": `delta = ${delta}, b = ${b}`})
            }
            let xk = x + Math.pow(2, k) * delta;
            print.push({"id": `5<sup>${k-1}</sup>`, "ans": `x<sup>k+1</sup> = x<sup>k</sup> + 2<sup>k</sup> * delta = ${xk}`})
            while (f(xk) < f(x)) {
                if (delta == eps) {
                    a = x;
                    print.push({"id": `6<sup>${k-1}</sup>`, "ans": `f(x<sup>k+1</sup>) = ${f(xk)}, f(x<sup>k</sup>) = ${f(x)}, a = ${a}`})
                }
                else {
                    b = x;
                    print.push({"id": `6<sup>${k-1}</sup>`, "ans": `f(x<sup>k+1</sup>) = ${f(xk)}, f(x<sup>k</sup>) = ${f(x)}, b = ${b}`})
                }

                x = xk;
                xk = x + Math.pow(2, k) * delta;
                k++;
                print.push({"id": `5<sup>${k-1}</sup>`, "ans": `x<sup>k+1</sup> = x<sup>k</sup> + 2<sup>k</sup> * delta = ${xk}`})
            }
            if (delta == eps) {
                b = xk;
            }
            else {
                a = xk;
            }
            print.push({"id": `6<sup>${k-1}</sup>`, "ans": `f(x<sup>k+1</sup>) = ${f(xk)}, f(x<sup>k</sup>) = ${f(x)}, a = ${a}, b = ${b}`})
            return [a, b];
        }
    }
    function fun(x: number) {
        return x * x - 4 * x + 7;
    }
    const eps: number = 0.5;
    const L: any = swann(fun, eps);
    const a: number = L[0];
    const b: number = L[1];
    const n = 100;

    function uniform_search(f: (x: number) => number, a: number, b: number, n: number): number {
        let points: number[] = [];
        for (let i: number = 0; i < n; ++i) {
            points.push(a + (b - a) / (n + 1));
        }
        let min: number = f(points[0]);
        let minx: number = points[0];
        for (let point: number in points) {
            let value: number = f(point);
            if (value < min) {
                min = value;
                minx = point;
            }
        }
        print.push({"id": `7`, "ans": `x<sub>*</sub> = ${minx} ∈ [${a}, ${b}], min = ${min}`})
        return minx;
    }
    let ans: number = uniform_search(fun, a, b, n);
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}
<h3>Ответ: x = {ans}</h3>
