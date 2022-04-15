<script lang="ts">
    function f(x: number): number {
        return x * x - 4 * x + 7;
    }
    const a = 0;
    const b = 10;
    const eps: number = 0.5;
    const del: number = 0.2;
    let print: object[] = [];
    let pred_pogr: number = 0;
    function dihotomiya(fun: (x: number) => number, a: number, b: number, eps: number, delta: number) {
        let i: number = 0;
        print.push({"id": "1<sup>0</sup>", "ans": `L<sub>0</sub> = [${a}, ${b}], l = ${eps * 2}, delta = ${delta}`});
        print.push({"id": "2<sup>0</sup>", "ans": `k = ${i}`});
        while (Math.abs(a - b) >= eps * 2) {
            let y: number = (a + b - delta) / 2;
            let z: number = (a + b + delta) / 2;
            let fy: number = fun(y);
            let fz: number = fun(z);
            print.push({"id": `3<sup>${i}</sup>`, "ans": `y<sub>${i}</sub> = (a<sub>${i}</sub> + b<sub>${i}</sub> - delta) / 2 = ${y}, z<sub>${i}</sub> = (a<sub>${i}</sub> + b<sub>${i}</sub> + delta) / 2 = ${z}, f(y<sub>${i}</sub>) = ${fy}, f(z<sub>${i}</sub>) = ${fz}`});
            if (fy < fz) {
                b = z;
            } else if (fy > fz) {
                a = y;
            }
            else {
                a = y;
                b = z;
            }

            print.push({"id": `4<sup>${i}</sup>`, "ans": `a<sub>${i+1}</sub> = ${a}, b<sub>${i+1}</sub> = ${b}`});
            print.push({"id": `6<sup>${i}</sup>`, "ans": `L<sup>${i+2}</sup> = [${a}, ${b}], |L|<sup>${i+2}</sup> = ${Math.abs(a - b)}, l = ${eps * 2}`});
            i++;
            pred_pogr = Math.abs(a - b) / 2;
        }
        return (a + b) / 2;
    }
    print = print;
    let ans: number = dihotomiya(f, a, b, eps, del);
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}
<h3>Ответ: x = {ans}, предельная погрешность = {pred_pogr}</h3>