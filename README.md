# Simulador GCP Finanzas — UMSA

**Estudiante:** Carlos Alejandro Salgado Llusco  
**Materia:** INF-373 — Métodos Numéricos I  
**Mención:** Desarrollo de Software e Innovación Tecnológica  
**Universidad:** Universidad Mayor de San Andrés

## Descripción
Aplicación web académica para modelar una distribución presupuestaria entre cuatro áreas de una empresa tecnológica y comparar Gradientes Conjugados (GC) con Gradientes Conjugados Precondicionados (GCP), utilizando Jacobi como precondicionador diagonal.

## Ejecutar localmente
1. Descarga o clona este repositorio.
2. Abre `index.html` en un navegador moderno.
3. No requiere instalación de dependencias ni servidor backend.
4. Selecciona un escenario, modifica los datos si lo deseas y presiona **Ejecutar cálculo**.
5. En el módulo QA, presiona **Ejecutar las 4 pruebas**.

También puedes ejecutar un servidor estático desde la carpeta:
```bash
python -m http.server 8000
```
Luego abre `http://localhost:8000`.

## Tecnologías
- HTML5
- CSS3
- JavaScript (ES6)
- Canvas 2D para el gráfico de convergencia

No se utilizan bibliotecas externas para resolver los sistemas: los algoritmos se implementan en el propio código JavaScript.

## Métodos implementados
- Factorización de Cholesky como solución directa de referencia.
- Gradientes Conjugados sin precondicionamiento.
- Gradientes Conjugados Precondicionados (PCG) con Jacobi diagonal.
- Verificación de simetría.
- Criterio de Sylvester mediante menores principales líderes.
- Número de condición 2 de A (matriz SPD).
- Número de condición 2 de M⁻¹A mediante valores singulares.
- Número de condición de la matriz simétrica equivalente M⁻¹/² A M⁻¹/².
- Errores absoluto, relativo y porcentual por variable.
- Residuo relativo global verdadero.

## Modelo y supuestos
Se modelan cuatro magnitudes presupuestarias, expresadas en miles de bolivianos:
- x1: Infraestructura tecnológica.
- x2: Desarrollo de software.
- x3: Seguridad informática.
- x4: Capacitación del personal.

Los coeficientes son datos sintéticos con fines académicos. La matriz A representa pesos relativos y acoplamientos del modelo cuadrático; b representa prioridades ponderadas. No se afirma que provengan de una empresa real. El modelo no incluye restricciones adicionales de no negatividad ni un presupuesto total fijo.

## Escenarios
- Ideal: matriz A1 y vector b1.
- Bajo estrés: conserva A1 y modifica b para representar menores prioridades/recursos.
- Mal condicionado: matriz simétrica SPD con escalas diagonales muy diferentes y precondicionador Jacobi.

En el escenario mal condicionado, la primera componente del vector b es **1595**. Se obtiene calculando A*x para x = [120, 150, 80, 60]ᵀ.

## Pruebas QA incluidas
1. Carga y resolución de los tres escenarios.
2. Rechazo de matriz no simétrica.
3. Edición dinámica de datos (prueba aislada con una copia temporal).
4. Comparación de iteraciones GC/GCP en el escenario mal condicionado.

## Publicar en GitHub Pages
1. Crea un repositorio público en GitHub.
2. Sube `index.html` y `README.md` a la raíz.
3. En Settings → Pages, elige desplegar desde la rama principal y la carpeta `/ (root)`.
4. Guarda y espera a que GitHub Pages publique el sitio.
5. Comparte la URL pública del sitio y la URL del repositorio.

## Bibliografía base del desafío
- Suñagua S., P. (2020). *Método de Gradientes Conjugados Precondicionado*. Revista Boliviana de Matemática – UMSA, 04, 2–7.
- Golub, G. H., & Van Loan, C. F. (2013). *Matrix Computations* (4th ed.). Johns Hopkins University Press.
- Saad, Y. (2003). *Iterative Methods for Sparse Linear Systems* (2nd ed.). SIAM.

## Nota para la defensa
Explicar que el precondicionador de Jacobi es M = diag(A), y en cada iteración se resuelve Mz = r mediante divisiones por los elementos diagonales. Para el escenario mal condicionado, comparar tanto κ₂(M⁻¹A) como el condicionamiento de la matriz simétrica equivalente M⁻¹/² A M⁻¹/². No confundir la solución numérica de referencia (Cholesky) con una solución algebraica exacta.
