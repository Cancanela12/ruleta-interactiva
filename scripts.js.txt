const opciones = ["Bebe un chupito", "Bebe 2 chupitos", "Beso"];
const colores = ["#FF5733", "#33FF57", "#3357FF"];

const canvas = document.getElementById("ruleta");
const ctx = canvas.getContext("2d");
const girarBtn = document.getElementById("girar");

const dibujarRuleta = () => {
    const anguloPorOpcion = 2 * Math.PI / opciones.length;
    opciones.forEach((opcion, index) => {
        const startAngle = index * anguloPorOpcion;
        const endAngle = startAngle + anguloPorOpcion;
        ctx.beginPath();
        ctx.moveTo(250, 250);
        ctx.arc(250, 250, 250, startAngle, endAngle);
        ctx.fillStyle = colores[index];
        ctx.fill();
        ctx.stroke();

        ctx.save();
        ctx.translate(250, 250);
        ctx.rotate(startAngle + anguloPorOpcion / 2);
        ctx.textAlign = "right";
        ctx.fillStyle = "#fff";
        ctx.font = "20px Arial";
        ctx.fillText(opcion, 240, 10);
        ctx.restore();
    });
};

const girarRuleta = () => {
    const anguloPorOpcion = 2 * Math.PI / opciones.length;
    const anguloAleatorio = Math.random() * 2 * Math.PI;
    const indiceGanador = Math.floor((anguloAleatorio + Math.PI / 2) / anguloPorOpcion) % opciones.length;

    canvas.style.transition = "transform 4s ease-out";
    canvas.style.transform = `rotate(${anguloAleatorio + 10 * 2 * Math.PI}rad)`;

    setTimeout(() => {
        alert(`¡Ha salido: ${opciones[indiceGanador]}!`);
        canvas.style.transition = "none";
        canvas.style.transform = `rotate(${anguloAleatorio % (2 * Math.PI)}rad)`;
    }, 4000);
};

girarBtn.addEventListener("click", girarRuleta);
dibujarRuleta();
