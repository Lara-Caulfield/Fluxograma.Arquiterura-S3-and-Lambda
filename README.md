# Fluxograma: Arquitetura S3 e Lambda 🏥💻

## Cenário
Os pacientes (usuários) solicitam exames, cada um com uma data específica.  
Esses exames foram guardados no **Amazon S3**, mas em **classes de Storage diferentes**:

- 📂 Exame com **2 meses** → está em **Standard** (acesso rápido).  
- 📂 Exame com **1 ano** → foi movido para **Glacier** (precisa de restauração).  

---

## Fluxo Básico
1. 🧑‍⚕️ **Paciente solicita o exame**.  
2. 📬 O pedido chega no **API Gateway**.  
3. ⚙️ O **Lambda** recebe a solicitação e pergunta ao **S3**:  
   > "Onde esse exame está armazenado?"  
4. 🔍 Decisão:
   - Se o exame está em **Standard** → Lambda gera o link e entrega direto ao paciente.  
   - Se o exame está em **Glacier** → Lambda responde:  
     > "Preciso descongelar o arquivo, por favor retorne mais tarde."  

---

## Componentes da Arquitetura
- **API Gateway** → porta de entrada para o paciente enviar o pedido.  
- **Lambda** → decide se entrega o exame ou inicia o processo de restauração.  
- **Amazon S3** → guarda os exames em diferentes classes de Storage.  
- **Email/Notificação** → informa o paciente quando o exame estará pronto para download.  

---

## Analogia Hospitalar 🏥
- **Standard** = exame guardado no balcão → entrega imediata.  
- **Glacier** = exame guardado no porão, dentro de um freezer → precisa descongelar antes.  
