<script lang="ts">

    function f(x: number) {
        return x * x - 4 * x + 7;
    }
    const a: number = 0;
    const b: number = 10;
    const eps: number = 0.5;
    const del: number = 0.2;
    let print: object[] = [];
    let pred_pogr: number = 0;
    function gold(fun: (x: number) => number, a: number, b: number, eps: number, del: number): number {
        let i: number = 0;
        const kor: number = (3 - Math.sqrt(5)) / 2;
        let y: number = a + (kor * (b - a));
        let z: number = a + b - y;
        print.push({"id": "1<sup>0</sup>", "ans": `L<sub>0</sub> = [${a}, ${b}], l = ${eps * 2}`});
        print.push({"id": "2<sup>0</sup>", "ans": `k = ${i}`})
        print.push({"id": "3<sup>0</sup>", "ans": `y<sub>0</sub> = a<sub>0</sub> + ${kor} * (b<sub>0</sub> - a<sub>0</sub>) = ${y}, z<sub>0</sub> = a<sub>0</sub> + b<sub>0</sub> - y<sub>0</sub> = ${z}`});
        do {
            let fy: number = fun(y);
            let fz: number = fun(z);
            print.push({"id": `4<sup>${i}</sup>`, "ans": `f(y<sup>${i}</sup>) = ${fy}, f(z<sup>${i}</sup>) = ${fz}`})
            if (fy <= fz) {
                b = z;
                z = y;
                y = a + b - y;
            }
            else {
                a = y;
                y = z;
                z = a + b - z;
            }
            print.push({"id": `5<sup>${i}</sup>`, "ans": `a<sup>${i+1}</sup> = ${a}, b<sup>${i+1}</sup> = ${b}, y<sup>${i+1}</sup>=${y}, z<sup>${i+1}</sup>=${z}`});
            print.push({"id": `6<sup>${i}</sup>`, "ans": `L<sup>${i+2}</sup> = [${a}, ${b}], |L|<sup>${i+2}</sup> = ${Math.abs(a - b)}, l = ${eps * 2}`});
            i++;
            pred_pogr = Math.abs(a - b) / 2;
        } while (Math.abs(a - b) >= 2 * eps)
        return (a + b) / 2;
    }
    let ans: number = gold(f, a, b, eps, del);
    print = print;
</script>

{#each print as p}
    <h3>Шаг {@html p.id}</h3>
    <p>{@html p.ans}</p>
{/each}
<h3>Ответ: x = {ans}, предельная погрешность = {pred_pogr}</h3>
