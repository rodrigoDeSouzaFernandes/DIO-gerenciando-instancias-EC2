# Anotações – Gerenciando instâncias ECS

---

## **1. Instâncias EC2 (Elastic Compute Cloud)**

### **O que é**
O Amazon EC2 é um dos principais serviços da AWS. Ele permite criar **máquinas virtuais** (chamadas de instâncias) que funcionam na nuvem. Essas instâncias podem executar diferentes sistemas operacionais (como Linux ou Windows) e são configuradas de acordo com as necessidades do usuário — por exemplo, quantidade de memória, CPU e armazenamento.

Na prática, uma instância EC2 funciona como um **servidor na nuvem**, usado para hospedar sites, aplicações web, bancos de dados, APIs ou qualquer outro tipo de software.

### **Pontos importantes**
- **Modelos de instância:** a AWS oferece vários tipos, como `t2.micro`, `m5.large`, `c5.xlarge`, etc., cada um voltado para um propósito (uso geral, computação intensiva, otimização de memória, entre outros).  
- **Regiões e Zonas de Disponibilidade:** as instâncias são criadas em regiões específicas. Isso afeta **latência**, **custo** e **disponibilidade**.  
- **Acesso:** é possível acessar a instância via **SSH** (para Linux) ou **RDP** (para Windows).  
- **Elastic IP:** permite associar um endereço IP fixo a uma instância, útil para servidores que precisam de endereço constante.  
- **Escalabilidade:** o EC2 trabalha com **Auto Scaling**, que aumenta ou reduz automaticamente o número de instâncias conforme a demanda.  
- **Cobrança:** o modelo é **pay-as-you-go**, ou seja, paga-se apenas pelo tempo em que a instância está ativa.  

Em resumo, o EC2 é a base de qualquer infraestrutura em nuvem dentro da AWS. Ele substitui a necessidade de comprar e manter servidores físicos, oferecendo flexibilidade e escalabilidade imediata.

---

## **2. Snapshots EBS (Elastic Block Store)**

### **O que é**
O EBS é o serviço de **armazenamento em blocos** usado pelas instâncias EC2. É o equivalente ao “disco rígido” (HD) da máquina virtual.  
Os **snapshots** são **cópias de segurança (backups)** de volumes EBS, permitindo restaurar dados em caso de falhas, corrompimentos ou exclusões acidentais.

Na prática, um snapshot é uma **foto do estado atual do volume EBS** em um determinado momento. Ele é armazenado automaticamente no Amazon S3, garantindo alta durabilidade e disponibilidade.

### **Pontos importantes**
- **Backup incremental:** após o primeiro snapshot completo, os próximos armazenam apenas as alterações feitas desde o último backup, economizando espaço e reduzindo custos.  
- **Restauração:** é possível criar um novo volume EBS a partir de um snapshot existente, recuperando rapidamente o sistema.  
- **Automação:** backups podem ser agendados de forma automática por meio do AWS Backup ou scripts usando a AWS CLI.  
- **Boas práticas:** sempre criar um snapshot antes de aplicar atualizações importantes no sistema ou alterar configurações críticas.  

Em termos práticos, snapshots são essenciais para garantir **continuidade de negócios** e **recuperação de desastres** em ambientes que dependem de EC2 e EBS.

---

## **3. AMI (Amazon Machine Image)**

### **O que é**
A AMI (Amazon Machine Image) é um **modelo de máquina virtual** que contém tudo o que é necessário para iniciar uma instância EC2. Ela inclui o **sistema operacional**, **aplicativos instalados**, **bibliotecas**, **configurações** e **permissões**.

Na prática, a AMI funciona como um “modelo pronto” usado para criar novas instâncias com a mesma configuração, garantindo padronização e agilidade na criação de servidores.

### **Pontos importantes**
- **Fontes de AMIs:**
  - **AMIs da AWS:** imagens oficiais e mantidas pela Amazon (ex.: Amazon Linux, Windows Server).  
  - **AMIs da comunidade:** criadas e compartilhadas por outros usuários.  
  - **AMIs personalizadas:** criadas pelo próprio usuário a partir de uma instância existente.  
- **Criação personalizada:** após configurar uma instância EC2 do jeito desejado (sistema, pacotes, segurança, etc.), é possível criar uma AMI dela para lançar outras instâncias idênticas.  
- **Regiões:** AMIs são **regionais**, sendo necessário copiá-las para outras regiões se quiser utilizá-las em diferentes locais.  
- **Privacidade:** podem ser **públicas** (compartilhadas) ou **privadas** (restritas à conta do criador).  
- **Uso em Auto Scaling:** ao usar escalabilidade automática, todas as novas instâncias são criadas a partir de uma AMI predefinida, garantindo consistência.  

Em resumo, a AMI é a base da automação na AWS. Ela permite replicar ambientes rapidamente e manter configurações padronizadas em larga escala.

---

### **Visão prática**
Na prática, o fluxo mais comum de uso desses serviços é o seguinte:
1. Criar uma **instância EC2** com o sistema operacional e configurações desejadas.  
2. Associar um **volume EBS** para armazenar dados.  
3. Criar **snapshots** periódicos para backup e recuperação.  
4. Gerar uma **AMI personalizada** para facilitar a criação de novas instâncias idênticas no futuro.

