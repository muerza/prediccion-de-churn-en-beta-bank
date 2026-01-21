🏦 Proyecto: Predicción de Churn en Beta Bank  

📌 Descripción general:

Los clientes de Beta Bank se están yendo, cada mes, poco a poco. Los banqueros descubrieron que es más barato salvar a los clientes existentes que atraer nuevos.

Necesitamos predecir si un cliente dejará el banco pronto. Tú tienes los datos sobre el comportamiento pasado de los clientes y la terminación de contratos con el banco.

Crea un modelo con el máximo valor F1 posible. Para aprobar la revisión, necesitas un valor F1 de al menos 0.59. Verifica F1 para el conjunto de prueba.

Además, debes medir la métrica AUC-ROC y compararla con el valor F1.

🎯 Objetivo
Crea un modelo con el máximo valor F1 posible. Para aprobar la revisión, necesitas un valor F1 de al menos 0.59. Verifica F1 para el conjunto de prueba.

📂 Descripción de los datos

🗂️ Fuente de datos

Archivo: /datasets/Churn.csv
🔢 Características (features)

RowNumber: índice de cadena de datos (número de fila)
CustomerId: identificador único del cliente
Surname: apellido del cliente
CreditScore: Score de crédito del cliente
Geography: país de residencia del cliente
Gender: sexo del cliente
Age: edad del cliente
Tenure: período durante el cual ha madurado el depósito a plazo fijo de un cliente (años)
Balance: saldo de la cuenta bancaria
NumOfProducts: número de productos bancarios utilizados por el cliente
HasCrCard: el cliente tiene una tarjeta de crédito
1 - sí
0 - no
IsActiveMember: actividad del cliente
1 - cliente activo
0 - cliente inactivo
EstimatedSalary: salario estimado del cliente
🎯 Variable objetivo

Exited: indica si el cliente se ha ido del banco
1 - el cliente se fue
0 - el cliente se quedó
0. Estrategia inicial

El objetivo principal es identificar a los clientes que tienen alta probabilidad de abandonar el banco.
Para ello, vamos a entrenar modelos de clasificación que aprendan a distinguir entre:

Clientes que se quedaron (Exited = 0).
Clientes que se fueron (Exited = 1).
