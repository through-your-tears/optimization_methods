<script lang="ts">
    function fun(x: number): number {
        return x * x - 4 * x + 7;
    }
    const a = 0;
    const b = 10;
    const eps: number = 0.5;
    const del: number = 0.2;
    let print: object[] = [];
    let pred_pogr: number = 0;
    function half_division(f: (x: number) => number, a: number, b: number, eps: number, delta: number) {
        let k: number = 0;
        let x_sr: number = (b + a) / 2;
        let L: number = b - a;
        let fk: number;
        print.push({"id": "1<sup>0</sup>", "ans": `L<sub>0</sub> = [${a}, ${b}], l = ${eps * 2}`});
        print.push({"id": "2<sup>0</sup>", "ans": `k = ${k}`})
        print.push({"id": "3<sup>0</sup>", "ans": `x<sub>k</sub><sup>c</sup> = ${x_sr}, |L<sub>${2 * k}</sub>| = ${L}`});
        do {
            fk = f(x_sr);
            let y: number = a + L / 4;
            let z: number = b - L / 4;
            print.push({"id": `4<sup>${k}</sup>`, "ans": `y<sub>${k}</sub> = ${y}, z<sub>${k}</sub> = ${z}`});
            if (f(y) < fk) {
                b = x_sr;
                x_sr = y;
                print.push({"id": `5<sup>${k}</sup>`, "ans": `b<sub>${k}</sub> = ${b}, x<sub>k</sub><sup>c</sup> = ${x_sr}`});
            } else {
                if (f(z) < fk) {
                    a = x_sr;
                    x_sr = z;
                } else {
                    a = y;
                    b = z;
                }
                print.push({"id": `6<sup>${k}</sup>`, "ans": `a<sub>${k}</sub> = ${a}, x<sub>k</sub><sup>c</sup> = ${x_sr}, b<sub>${k}</sub> = ${b}`});
            }
            L = Math.abs(b - a);
            print.push({"id": `7<sup>${k}</sup>`, "ans": `L<sub>${2 * k}</sub> = ${L}, k = ${k}`});
            k++;
        } while (Math.abs(L) > 2 * eps);
        pred_pogr = Math.abs(a - b) / 2;
        return x_sr;
    }
    let ans:number = half_division(fun, a, b, eps, del);
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}
<h3>Ответ: x = {ans}, предельная погрешность = {pred_pogr}</h3>