---
title: Adquirir e configurar um servidor de Backup para PDW APS
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Configure um sistema do Windows não seja de aplicação como um servidor de backup para uso com o backup e restaurar recursos no Analytics Platform System (APS) e SQL Server Parallel Data Warehouse (PDW)."
ms.date: 10/20/2016
ms.topic: article
caps.latest.revision: "20"
ms.assetid: f8b769fe-c864-4d65-abcb-a9a287061702
ms.openlocfilehash: 3540c2e43082dbdad4f267745683f33ae9b0b036
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="acquire-and-configure-a-backup-server"></a>Adquirir e configurar um servidor de backup
Este tópico descreve como configurar um sistema do Windows não seja de aplicação como um servidor de backup para uso com os recursos de backup e restauração no Analytics Platform System (APS) e SQL Server Parallel Data Warehouse (PDW).  
  
  
## <a name="Basics"></a>Noções básicas de servidor de backup  
O servidor de backup:  
  
-   É fornecido e gerenciados pela sua equipe de TI.  
  
-   Não requer qualquer software específicas do PDW ou ferramentas. PDW não instale o software no servidor de backup.  
  
-   Está localizado em seu próprio dispositivo não rack e não pode ser colocado no dispositivo APS.  
  
-   Pode ser conectado à rede InfiniBand appliance. Os backups podem ser executados com InfiniBand ou Ethernet; InfiniBand é recomendado por razões de desempenho.  
  
-   Está em seu próprio domínio de cliente, não o domínio de aplicativo. Não há nenhuma relação de confiança entre o domínio de cliente e o domínio de aplicativo.  
  
-   Hospeda um compartilhamento de arquivo de backup, que é um compartilhamento de arquivos do Windows que usa o protocolo de rede no nível de aplicativo do bloco de mensagens de servidor (SMB). As permissões de compartilhamento de arquivo de backup conceder a um usuário de domínio do Windows (geralmente, isso é um usuário de backup dedicado) a capacidade de realizar backup e restaurar operações no compartilhamento. As credenciais de usuário e senha do usuário de domínio do Windows são armazenadas no PDW para que o PDW pode realizar o backup e restaurar operações no compartilhamento de arquivo de backup.  
  
## <a name="Step1"></a>Etapa 1: Determinar os requisitos de capacidade  
Os requisitos de sistema para o servidor de Backup quase que totalmente dependem de sua carga de trabalho. Antes de adquirir ou provisionamento de um servidor de backup, você precisa descobrir seus requisitos de capacidade. O servidor de Backup não precisa ser dedicada somente para backups, como ele tratará os requisitos de armazenamento e o desempenho da carga de trabalho. Você também pode ter vários servidores de backup para backup e restauração de cada banco de dados para um dos vários servidores.  
  
Use o [planilha de planejamento de capacidade do Backup server](backup-capacity-planning-worksheet.md) para ajudar a determinar seus requisitos de capacidade.  
  
## <a name="Step2"></a>Etapa 2: Adquirir o servidor de backup  
Agora que você entender melhor os seus requisitos de capacidade, você pode planejar os servidores e os componentes de rede que você precisará comprar ou provisionar. Incorporar a seguinte lista de requisitos de seu plano de compra, compra seu servidor ou provisionar um servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Qualquer servidor de arquivos que usa o protocolo de compartilhamento de arquivo do Windows (SMB).  
  
Recomendamos que o Windows Server 2012 ou além para:  
  
-   Obter o benefício de desempenho de pré-alocação de arquivo no SMB.  
  
-   Use a inicialização instantânea de arquivo (IFI) para operações de backup. Sua equipe de TI gerencia essa configuração no servidor de backup. O Gerenciador de configuração do PDW (dwconfig.exe) não definido ou controle IFI no servidor de backup. Versões anteriores do Windows não têm IFI, mas ainda podem ser usadas como servidores de backup.  
  
### <a name="networking-requirements"></a>Requisitos de rede  
Embora não seja necessário, InfiniBand é o tipo de conexão recomendado para servidores de Backup. Para preparar para conectar o servidor ao carregar a rede InfiniBand dispositivo:  
  
1.  Planejar o servidor de rack aproximados o suficiente para o dispositivo para que você pode conectá-lo para o dispositivo alterna InfiniBand. Para saber mais sobre InfiniBand Mellanox tecnologias, consulte o white paper, [Introdução ao InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre um adaptador de rede de porta única ou dupla Mellanox ConnectX-3 FDR InfiniBand. Recomendamos que você comprar o adaptador de rede com duas portas para tolerância a falhas durante a transmissão de dados. Um adaptador de rede de duas portas é necessário para alta disponibilidade.  
  
3.  Compre 2 cabos FDR InfiniBand para uma placa de porta dupla ou 1 cabo FDR InfiniBand para uma placa de porta única. Os cabos FDR InfiniBand conectará o carregando o servidor à rede InfiniBand appliance. O comprimento de cabo depende da distância entre o servidor de carregamento e as opções do dispositivo InfiniBand, acordo com seu ambiente.  
  
## <a name="Step3"></a>Etapa 3: Conectar o servidor para as redes InfiniBand  
Use estas etapas para conectar o servidor ao carregar a rede InfiniBand. Se o servidor não estiver usando a rede InfiniBand, ignore esta etapa.  
  
1.  O servidor de rack feche suficiente para o dispositivo para que você pode conectá-lo à rede InfiniBand appliance.  
  
2.  Instale o adaptador de rede InfiniBand Mellanox ConnectX-3 FDR InfiniBand para o servidor de carregamento.  
  
3.  Use os cabos FDR para conectar o adaptador de rede InfiniBand para uma das duas opções InfiniBand no primeiro rack do dispositivo.  
  
4.  Instale e configure o driver apropriado do Windows para o adaptador de rede InfiniBand.  
  
    -   InfiniBand drivers do Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio do setor de fornecedores de InfiniBand.  O driver correto pode foram distribuído com o adaptador de rede InfiniBand. Caso contrário, o driver pode ser baixado do www.openfabrics.org.  
  
5.  Defina as configurações de DNS e InfiniBand para os adaptadores de rede. Para obter instruções de configuração, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Etapa 4: Configurar o compartilhamento de arquivo de backup  
PDW acessará o servidor de backup por meio de um compartilhamento de arquivo UNC. Para configurar o compartilhamento de arquivos:  
  
1.  Crie uma pasta no servidor de backup para armazenar seus backups.  
  
2.  Crie um compartilhamento de arquivo, chamado de um compartilhamento de backup para a pasta de backup.  
  
3.  Designar ou criar uma conta de domínio do Windows no seu domínio do cliente que você deseja usar para fins de execução de backups e restaurações. Por motivos de segurança, é melhor usar uma conta dedicada como o usuário de backup.  
  
4.  Adicione permissões para o backup do compartilham para que possam acessar somente contas confiáveis e uma conta de domínio de backup, ler e gravar no local de compartilhamento.  
  
5.  Adicione as credenciais da conta de domínio de backup para o PDW.  
  
    Por exemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obter mais informações, consulte esses procedimentos armazenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Etapa 5: Iniciar o backup dos dados  
Agora você está pronto para começar a fazer backup de dados para o servidor de backup.  
  
Para fazer backup de dados, use um cliente consulta para se conectar ao SQL Server PDW e, em seguida, enviar o BACKUP ou RESTAURAR banco comandos. Usar o disco = cláusula para especificar o local de backup e o servidor de Backup.  
  
> [!IMPORTANT]  
> Lembre-se de usar o endereço IP do InfiniBand do servidor de backup. Caso contrário, os dados serão copiados na Ethernet em vez de InfiniBand.  
  
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
O servidor de backup não está unido ao domínio particular para o dispositivo. Ele está em sua própria rede e não há nenhuma relação de confiança entre seu próprio domínio e privada do dispositivo.  
  
Como backups PDW não são armazenados no dispositivo, sua equipe de TI é responsável por gerenciar todos os aspectos de segurança do backup. Por exemplo, isso inclui a gerenciar a segurança de dados de backup, a segurança do servidor usado para armazenar backups e a segurança da infraestrutura de rede que conecta o servidor de backup para o dispositivo de APS.  
  
### <a name="manage-network-credentials"></a>Gerenciar credenciais de rede  
  
Acesso à rede para o diretório de backup baseia-se a segurança de compartilhamento de arquivos de Windows padrão. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar o PDW para o diretório de backup. Essa conta do windows deve ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
> Para reduzir os riscos de segurança com seus dados, é recomendável que você designa uma conta do Windows exclusivamente para fins de execução de backups e operações de restauração. Permitir que essa conta tem permissões para o local de backup e em nenhum outro lugar.  
  
Para armazenar o nome de usuário e senha PDW, use o [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimento armazenado. PDW usa o Gerenciador de credenciais do Windows para armazenar e criptografar os nomes de usuário e senhas no nó de controle e nós de computação. As credenciais não contam com o comando de banco de dados de BACKUP.  
  
Para remover as credenciais de rede do PDW, use o [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) procedimento armazenado.  
  
Para listar todas as credenciais de rede armazenadas no SQL Server PDW, use o [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) exibição de gerenciamento dinâmico.  
  
### <a name="secure-communications"></a>Comunicações seguras  
  
Operações no servidor de carregamento podem usar um caminho UNC para extrair dados de fora da rede interna confiável. Um invasor na rede ou com capacidade para influenciar a resolução de nomes pode interceptar ou modificar os dados enviados para o PDW. Isso apresenta um risco de divulgação de violação e informações. Para ajudar a reduzir o risco de violação:

- Exigir assinatura em que a conexão. 
- No servidor do carregamento, defina a opção de política de grupo a seguir nas opções de diretivas de configurações de segurança: o cliente de rede Microsoft: assinar comunicações digitalmente (sempre): habilitado.  
  
## <a name="see-also"></a>Consulte também  
[Backup e restauração](backup-and-restore-overview.md)  
  
