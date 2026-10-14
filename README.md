# Investigação de E-mail Falso *Phishing* e *Malwares*

![MxToolbox](https://img.shields.io/badge/MxToolbox-005B9F?style=for-the-badge)
![VirusTotal](https://img.shields.io/badge/VirusTotal-394EFF?style=for-the-badge&logo=virustotal&logoColor=white)
![CyberChef](https://img.shields.io/badge/CYBERCHEF-A020F0?style=for-the-badge)
![ANY.RUN](https://img.shields.io/badge/ANY.RUN-00A6E7?style=for-the-badge)

Este laboratório prático foi desenvolvido com base no desafio oficial [CyberDefenders](cyberdefenders.org/) simulando um cenário real onde professores recebem um e-mail que parece de um contato confiavel e reivindica uma compra de valor alto. 
A resolução teve como foco a aplicação de Blue Team, investigação de incidentes e análise de malwares.

### Visão Geral

- **Alerta de Phishing:** Um e-mail falso cobrando uma fatura de US$ 625.000 foi enviado aos professores da escola.
- **Rastreio da origem:** Análise dos cabeçalhos do e-mail para comprovar a falsificação da identidade do remetente.
- **Descoberta do vírus:** Investigação do link malicioso para encontrar o servidor do invasor e o arquivo perigoso.
- **Análise do disfarce:** Decodificação do código do vírus para entender como ele "dorme" para enganar os antivírus.

---

### Laboratório e Preparação

Para a execução da análise, utilizei ferramentas e plataformas baseadas em inteligência de ameaças (Threat Intelligence):

- **MxToolbox:** Para analisar o código por trás do e-mail (cabeçalhos) e descobrir se o remetente era falso.
- **VirusTotal:** Para investigar a reputação do link perigoso e ver o histórico de como o vírus age no computador.
- **CyberChef:** Ferramenta para traduzir e desembaralhar os códigos escondidos pelo invasor.
- **ANY.RUN:** Máquina virtual de testes (Sandbox) para tentar ver o vírus agindo ao vivo.

---

### 1. Rastreando a origem do e-mail

A primeira coisa que fiz foi olhar o código por trás do e-mail (cabeçalho). Descobri que ele reprovou nos testes de segurança (falhou no SPF e DKIM), provando que o remetente era falso.

<img width="1321" height="654" alt="image" src="https://github.com/user-attachments/assets/b61cbc99-debd-4c9a-87c8-34125bf750dd" />



---

### 2. Descobrindo de onde o vírus vinha

Peguei o link perigoso que estava no e-mail e pesquisei no VirusTotal. Descobri que o link tentava baixar um arquivo chamado `install.exe` de um servidor malicioso (IP 107.175.247.199).

<img width="1321" height="654" alt="image" src="https://github.com/user-attachments/assets/b55488a8-62e3-42b4-9c4f-0f7b38dbe365" />

---

### 3. Histórico de Conexões do Arquivo

Vários antivírus confirmaram que o arquivo era perigoso. Vasculhando o histórico de ações do vírus, foi possível ver os links exatos com os quais ele tentava se comunicar.

<img width="1321" height="654" alt="Opera Instantâneo_2026-10-12_200237_app any run" src="https://github.com/user-attachments/assets/3366d008-a946-40d9-b797-09ea89ae91cc" />

---

### 4. O truque para enganar o antivírus

Vírus espertos tentam se disfarçar. Olhando o histórico de ações, vi que ele abriu o Windows PowerShell e usou um código texto todo embaralhado, além de criar um arquivo `Jzwvix.exe` para ficar escondido no PC para sempre.

<img width="1321" height="654" alt="image" src="https://github.com/user-attachments/assets/c28b1060-a4c1-489b-a6a1-b91bed1e503b" />

---

### 5. Desembaralhando o código oculto

Para provar o que o código fazia, usei a ferramenta CyberChef. O resultado desembaralhado mostrou o comando `Start-Sleep -Seconds 50`, comprovando que o vírus "dorme" (pausa) por 50 segundos para despistar os sistemas de defesa!

<img width="1321" height="654" alt="Opera Instantâneo_2026-10-12_204921_gchq github io" src="https://github.com/user-attachments/assets/98f9abd8-6d47-478a-9a5d-b6e728b82fba" />


---

### Conclusão

Nesta investigação prática, foi possível atingir os seguintes resultados:

- Rastreio com sucesso da origem do e-mail falso provando a fraude.
- Identificação exata de como o vírus agia (escondendo-se e pausando por 50 segundos para evitar detecção).
- Coleta de provas e Indicadores de Comprometimento (IPs e links perigosos).

@2026 Gisele Alencar
