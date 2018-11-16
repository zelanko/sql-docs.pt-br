---
title: Adquirir e configurar um servidor de backup – Parallel Data Warehouse | Microsoft Docs
description: Este artigo descreve como configurar um sistema do Windows não seja de dispositivo como um servidor de backup para uso com os recursos de backup e restauração no Analytics Platform System (APS) e o Parallel Data Warehouse (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cba345eb7a5aec9ef857819a1f0499266649f6e4
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696945"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Adquirir e configurar um servidor de backup para Parallel Data Warehouse
Este artigo descreve como configurar um sistema do Windows não seja de dispositivo como um servidor de backup para uso com os recursos de backup e restauração no Analytics Platform System (APS) e o Parallel Data Warehouse (PDW).  
  
  
## <a name="Basics"></a>Noções básicas do servidor de backup  
O servidor de backup:  
  
-   É fornecido e gerenciado por sua própria equipe de TI.  
  
-   Não exige qualquer software PDW específicas ou ferramentas. PDW não instalar nenhum software no servidor de backup.  
  
-   Está localizado em seu próprio rack não seja de dispositivo e não podem ser colocados dentro de dispositivo de APS.  
  
-   Pode ser conectado à rede InfiniBand appliance. Backups podem ser executados com InfiniBand ou Ethernet; InfiniBand é recomendado por motivos de desempenho.  
  
-   Está em seu próprio domínio de cliente, não o domínio do dispositivo. Não há nenhuma relação de confiança entre seu domínio de cliente e o domínio do dispositivo.  
  
-   Hospeda um compartilhamento de arquivo de backup, que é um compartilhamento de arquivos do Windows que usa o protocolo de rede de nível de aplicativo do bloco de mensagens de servidor (SMB). As permissões de compartilhamento de arquivo de backup conceder a um usuário de domínio do Windows (normalmente, esse é um usuário de backup dedicada) a capacidade de realizar backup e restaurar operações no compartilhamento. As credenciais de nome de usuário e senha do usuário de domínio do Windows são armazenadas no PDW para que o PDW pode realizar backup e restaurar operações no compartilhamento de arquivo de backup.  
  
## <a name="Step1"></a>Etapa 1: Determinar os requisitos de capacidade  
Requisitos do sistema para o servidor de Backup quase que totalmente dependem de sua própria carga de trabalho. Antes de adquirir ou o provisionamento de um servidor de backup, você precisa descobrir seus requisitos de capacidade. O servidor de Backup não precisa ser dedicada somente para backups, desde que ele manipulará os requisitos de armazenamento e o desempenho da carga de trabalho. Você também pode ter vários servidores de backup para fazer backup e restaurar cada banco de dados para um dos vários servidores.  
  
Use o [planilha de planejamento de capacidade do Backup servidor](backup-capacity-planning-worksheet.md) para ajudar a determinar os requisitos de capacidade.  
  
## <a name="Step2"></a>Etapa 2: Adquirir o servidor de backup  
Agora que você entende melhor os requisitos de capacidade, você pode planejar os servidores e componentes de rede que será necessário comprar ou provisionar. Incorporar a lista dos requisitos a seguir em seu plano de compra e, em seguida, comprar seu servidor ou provisionar um servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Qualquer servidor de arquivos que usa o protocolo de compartilhamento de arquivo do Windows (SMB).  
  
Recomendamos que o Windows Server 2012 ou além para:  
  
-   Obter o benefício de desempenho de pré-alocação de arquivos via SMB.  
  
-   Use o arquivo IFI (inicialização instantânea) para operações de backup. Sua equipe de TI gerencia essa configuração no servidor de backup. O Gerenciador de configuração do PDW (dwconfig.exe) Configure nem controlar IFI no seu servidor de backup. As versões anteriores do Windows não têm a IFI, mas ainda podem ser usadas como servidores de backup.  
  
### <a name="networking-requirements"></a>Requisitos de rede  
Embora não seja necessário, o InfiniBand é o tipo de conexão recomendado para servidores de Backup. Para preparar para conectar o servidor de carregamento para a rede InfiniBand de dispositivo:  
  
1.  Planejar para o servidor de rack aproximados o suficiente para o dispositivo para que você pode conectá-lo para o dispositivo alterna InfiniBand. Para obter mais informações de tecnologias Mellanox InfiniBand, consulte o white paper, [Introdução ao InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre um adaptador de rede Mellanox ConnectX-3 FDR InfiniBand porta único ou duplo. É recomendável adquirir o adaptador de rede com duas portas para tolerância a falhas durante a transmissão de dados. Um adaptador de rede de duas portas é necessário para alta disponibilidade.  
  
3.  2 cabos FDR InfiniBand para um cartão de porta dupla ou 1 cabo FDR InfiniBand para um cartão de porta única de compra. Os cabos de InfiniBand FDR conectará o servidor de carregamento para a rede InfiniBand de solução de virtualização. O comprimento de cabo depende da distância entre o servidor de carregamento e os comutadores de InfiniBand appliance, acordo com seu ambiente.  
  
## <a name="Step3"></a>Etapa 3: Conectar o servidor para as redes InfiniBand  
Use estas etapas para conectar o servidor de carregamento para a rede InfiniBand. Se o servidor não estiver usando a rede InfiniBand, ignore esta etapa.  
  
1.  O servidor de rack feche suficiente para o dispositivo para que você pode conectá-lo à rede InfiniBand appliance.  
  
2.  Instale o adaptador de rede InfiniBand Mellanox ConnectX-3 FDR InfiniBand para o servidor de carregamento.  
  
3.  Use os cabos FDR para conectar o adaptador de rede InfiniBand para um dos dois switches de InfiniBand no primeiro rack do dispositivo.  
  
4.  Instale e configure o driver apropriado do Windows para o adaptador de rede InfiniBand.  
  
    -   Drivers de InfiniBand para Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio do setor de fornecedores de InfiniBand.  O driver correto pode foram distribuído com o adaptador de rede InfiniBand. Caso contrário, o driver pode ser baixado em www.openfabrics.org.  
  
5.  Defina as configurações de DNS e InfiniBand para os adaptadores de rede. Para obter instruções de configuração, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Etapa 4: Configurar o compartilhamento de arquivo de backup  
PDW acessará o servidor de backup por meio de um compartilhamento de arquivo UNC. Para configurar o compartilhamento de arquivos:  
  
1.  Crie uma pasta no servidor de backup para armazenar seus backups.  
  
2.  Crie um compartilhamento de arquivo, chamado de um compartilhamento de backup para a pasta de backup.  
  
3.  Designe ou crie uma conta de domínio do Windows no seu domínio do cliente que você deseja usar para fins de execução de backups e restaurações. Por motivos de segurança, é melhor usar uma conta dedicada como o usuário de backup.  
  
4.  Adicione permissões para o backup compartilham para que possam acessar apenas as contas confiáveis e uma conta de domínio de backup, ler e gravar no local de compartilhamento.  
  
5.  Adicione as credenciais da conta de domínio de backup para o PDW.  
  
    Por exemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obter mais informações, consulte esses procedimentos armazenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Etapa 5: Iniciar o backup dos dados  
Agora você está pronto para começar a fazer backup dos dados para o servidor de backup.  
  
Para fazer backup de dados, use um cliente de consulta para se conectar ao SQL Server PDW e, em seguida, enviar BACKUP banco de dados ou RESTAURAR banco de dados de comandos. Use o disco = cláusula para especificar o local de backup e o servidor de Backup.  
  
> [!IMPORTANT]  
> Lembre-se de usar o endereço IP do InfiniBand do servidor de backup. Caso contrário, os dados serão copiados pela Ethernet em vez de InfiniBand.  
  
Por exemplo:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Para obter mais informações, consulte: 
  
-   [BANCO DE DADOS DE BACKUP](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTAURAR BANCO DE DADOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Avisos de segurança  
O servidor de backup não está unido ao domínio particular para o dispositivo. Ele está em sua própria rede, e não há nenhuma relação de confiança entre seu próprio domínio e privadas de dispositivo.  
  
Uma vez que os backups PDW não são armazenados no dispositivo, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança do backup. Por exemplo, isso inclui gerenciar a segurança de dados de backup, a segurança do servidor usado para armazenar os backups e a segurança da infraestrutura de rede que conecta o servidor de backup para o dispositivo de APS.  
  
### <a name="manage-network-credentials"></a>Gerenciar credenciais de rede  
  
O acesso da rede ao diretório de backup baseia-se na segurança de compartilhamento de arquivos padrão do Windows. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar o PDW para o diretório de backup. Essa conta do Windows precisa ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
> Para reduzir os riscos de segurança para seus dados, é recomendável designar uma conta do Windows exclusivamente para a finalidade de executar operações de backup e restauração. Permita que essa conta tenha permissões para o local de backup e não tenha para nenhum outro lugar.  
  
Para armazenar o nome de usuário e a senha no PDW, use o [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento armazenado. PDW usa o Gerenciador de credenciais do Windows para armazenar e criptografar os nomes de usuário e senhas no nó de controle e nós de computação. As credenciais não são submetidas a backup com o comando BACKUP DATABASE.  
  
Para remover as credenciais de rede do PDW, use o [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) procedimento armazenado.  
  
Para listar todas as credenciais de rede armazenadas no SQL Server PDW, use o [DM pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) exibição de gerenciamento dinâmico.  
  
### <a name="secure-communications"></a>Comunicações seguras  
  
Operações no servidor de carregamento podem usar um caminho UNC para extrair dados de fora da rede interna confiável. Um invasor na rede ou com capacidade para influenciar a resolução de nomes pode interceptar ou modificar os dados enviados para o PDW. Isso apresenta um risco de divulgação de informações e falsificação. Para ajudar a reduzir o risco de violação:

- Exigem a conexão de assinatura. 
- No servidor de carregamento, defina a seguinte opção de diretiva de grupo em segurança Settings\Local Policies\Security Options: cliente de rede Microsoft: assinar comunicações digitalmente (sempre): habilitado.  
  
## <a name="see-also"></a>Consulte também  
[Backup e restauração](backup-and-restore-overview.md)  
  
