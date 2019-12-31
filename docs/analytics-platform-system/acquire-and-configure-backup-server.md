---
title: Adquirir & configurar o servidor de backup
description: Este artigo descreve como configurar um sistema Windows que não seja de dispositivo como um servidor de backup para uso com os recursos de backup e restauração no sistema de plataforma de análise (PAS) e data warehouse em paralelo (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e160c606b19933934ec844b477ffec08475307d8
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401492"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Adquirir e configurar um servidor de backup para data warehouse paralelos
Este artigo descreve como configurar um sistema Windows que não seja de dispositivo como um servidor de backup para uso com os recursos de backup e restauração no sistema de plataforma de análise (PAS) e data warehouse em paralelo (PDW).  
  
  
## <a name="Basics"></a>Noções básicas do servidor de backup  
O servidor de backup:  
  
-   É fornecido e gerenciado por sua própria equipe de ti.  
  
-   Não requer software ou ferramentas específicas do PDW. O PDW não instala nenhum software no servidor de backup.  
  
-   O está localizado em seu próprio rack que não é de dispositivo e não pode ser colocado dentro do dispositivo APS.  
  
-   Pode ser conectado à rede InfiniBand do dispositivo. Os backups podem ser executados em InfiniBand ou Ethernet; A InfiniBand é recomendada por motivos de desempenho.  
  
-   Está em seu próprio domínio de cliente, não no domínio do dispositivo. Não há nenhuma relação de confiança entre o domínio do cliente e o domínio do dispositivo.  
  
-   Hospeda um compartilhamento de arquivos de backup, que é um compartilhamento de arquivos do Windows que usa o protocolo de rede de nível de aplicativo SMB (bloco de mensagens do servidor). As permissões de compartilhamento de arquivo de backup fornecem a um usuário de domínio do Windows (geralmente esse é um usuário de backup dedicado) a capacidade de executar operações de backup e restauração no compartilhamento. As credenciais de nome de usuário e senha dos usuários de domínio do Windows são armazenadas no PDW para que o PDW possa executar operações de backup e restauração no compartilhamento de arquivos de backup.  
  
## <a name="Step1"></a>Etapa 1: determinar os requisitos de capacidade  
Os requisitos de sistema para o servidor de backup dependem quase completamente da sua própria carga de trabalho. Antes de comprar ou provisionar um servidor de backup, você precisa descobrir seus requisitos de capacidade. O servidor de backup não precisa ser dedicado apenas a backups, desde que ele lide com os requisitos de desempenho e armazenamento de sua carga de trabalho. Você também pode ter vários servidores de backup para fazer backup e restaurar cada banco de dados em um de vários servidores.  
  
Use a [planilha de planejamento de capacidade do servidor de backup](backup-capacity-planning-worksheet.md) para ajudar a determinar os requisitos de capacidade.  
  
## <a name="Step2"></a>Etapa 2: adquirir o servidor de backup  
Agora que você entende melhor seus requisitos de capacidade, é possível planejar os servidores e os componentes de rede que precisará comprar ou provisionar. Incorpore a lista de requisitos a seguir em seu plano de compra e, em seguida, adquira o servidor ou provisione um servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Qualquer servidor de arquivos que usa o protocolo SMB (compartilhamento de arquivos do Windows).  
  
Recomendamos o Windows Server 2012 ou posterior para:  
  
-   Obtenha o benefício de desempenho da pré-alocação de arquivos em relação ao SMB.  
  
-   Use a IFI (inicialização instantânea de arquivo) para operações de backup. Sua equipe de ti gerencia essa configuração no servidor de backup. O Configuration Manager do PDW (dwconfig. exe) não define ou controla IFI no servidor de backup. As versões anteriores do Windows não têm IFI, mas ainda podem ser usadas como servidores de backup.  
  
### <a name="networking-requirements"></a>Requisitos de rede  
Embora não seja necessário, o InfiniBand é o tipo de conexão recomendado para servidores de backup. Para se preparar para conectar o servidor de carregamento à rede InfiniBand do dispositivo:  
  
1.  Planeje o servidor para o dispositivo fechar o suficiente para que você possa conectá-lo aos comutadores InfiniBand do dispositivo. Para obter mais informações sobre as tecnologias Mellanox sobre InfiniBand, consulte o White Paper, [introdução ao InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre um adaptador de rede de porta única ou dual de Mellanox ConnectX-3 FDR InfiniBand. É recomendável adquirir o adaptador de rede com duas portas para tolerância a falhas durante a transmissão de dados. Um adaptador de rede de duas portas é necessário para alta disponibilidade.  
  
3.  Adquira 2 cabos de InfiniBand FDR para uma placa de porta dupla ou um cabo InfiniBand de 1 FDR para um cartão de porta única. Os cabos do FDR InfiniBand conectarão o servidor de carregamento à rede InfiniBand do dispositivo. O comprimento do cabo depende da distância entre o servidor de carregamento e os comutadores InfiniBand do dispositivo, de acordo com seu ambiente.  
  
## <a name="Step3"></a>Etapa 3: conectar o servidor às redes InfiniBand  
Use estas etapas para conectar o servidor de carregamento à rede InfiniBand. Se o servidor não estiver usando a rede InfiniBand, ignore esta etapa.  
  
1.  Rack o servidor está perto o suficiente para o dispositivo para que você possa conectá-lo à rede InfiniBand do dispositivo.  
  
2.  Instale o adaptador de rede InfiniBand de InfiniBand ConnectX-3 FDR com o servidor de carregamento.  
  
3.  Use os cabos FDR para conectar o adaptador de rede InfiniBand a um dos dois comutadores InfiniBand no primeiro rack do dispositivo.  
  
4.  Instale e configure o driver do Windows apropriado para o adaptador de rede InfiniBand.  
  
    -   Os drivers InfiniBand para Windows são desenvolvidos pela OpenFabrics Alliance, um consórcio da indústria de fornecedores InfiniBand.  O driver correto pode ter sido distribuído com o adaptador de rede InfiniBand. Caso contrário, o driver pode ser baixado em www.openfabrics.org.  
  
5.  Defina as configurações de InfiniBand e DNS para os adaptadores de rede. Para obter instruções de configuração, consulte [configurar adaptadores de rede InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Etapa 4: configurar o compartilhamento de arquivos de backup  
O PDW acessará o servidor de backup por meio de um compartilhamento de arquivos UNC. Para configurar o compartilhamento de arquivos:  
  
1.  Crie uma pasta no servidor de backup para armazenar seus backups.  
  
2.  Crie um compartilhamento de arquivos, chamado de compartilhamento de backup, para a pasta de backup.  
  
3.  Designe ou crie uma conta de domínio do Windows no domínio do cliente que você deseja usar para realizar backups e restaurações. Por motivos de segurança, é melhor usar uma conta dedicada como o usuário de backup.  
  
4.  Adicione permissões ao compartilhamento de backup para que somente contas confiáveis e uma conta de backup de domínio possam acessar, ler e gravar no local de compartilhamento.  
  
5.  Adicione as credenciais da conta de domínio de backup ao PDW.  
  
    Por exemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obter mais informações, consulte estes procedimentos armazenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Etapa 5: iniciar o backup dos dados  
Agora você está pronto para iniciar o backup de dados no servidor de backup.  
  
Para fazer backup de dados, use um cliente de consulta para se conectar ao SQL Server PDW e, em seguida, enviar o banco de dados de BACKUP ou restaurar os comandos do banco Use a cláusula DISK = para especificar o servidor de backup e o local de backup.  
  
> [!IMPORTANT]  
> Lembre-se de usar o endereço IP de InfiniBand do servidor de backup. Caso contrário, os dados serão copiados pela Ethernet em vez de InfiniBand.  
  
Por exemplo:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Para obter mais informações, consulte: 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Avisos de segurança  
O servidor de backup não está ingressado no domínio privado do dispositivo. Ele está em sua própria rede e não há nenhuma relação de confiança entre seu próprio domínio e domínio de dispositivo privado.  
  
Como os backups do PDW não são armazenados no dispositivo, sua equipe de ti é responsável por gerenciar todos os aspectos da segurança de backup. Por exemplo, isso inclui o gerenciamento da segurança dos dados de backup, a segurança do servidor usado para armazenar backups e a segurança da infraestrutura de rede que conecta o servidor de backup ao dispositivo APS.  
  
### <a name="manage-network-credentials"></a>Gerenciar credenciais de rede  
  
O acesso da rede ao diretório de backup baseia-se na segurança de compartilhamento de arquivos padrão do Windows. Antes de executar um backup, você precisa criar ou designar uma conta do Windows que será usada para autenticar o PDW para o diretório de backup. Essa conta do Windows precisa ter permissão para acessar, criar e gravar no diretório de backup.  
  
> [!IMPORTANT]  
> Para reduzir os riscos de segurança para seus dados, é recomendável designar uma conta do Windows exclusivamente para a finalidade de executar operações de backup e restauração. Permita que essa conta tenha permissões para o local de backup e não tenha para nenhum outro lugar.  
  
Para armazenar o nome de usuário e a senha no PDW, use o procedimento armazenado [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) . O PDW usa o Gerenciador de credenciais do Windows para armazenar e criptografar nomes de usuário e senhas no nó de controle e nos nós de computação. As credenciais não são submetidas a backup com o comando BACKUP DATABASE.  
  
Para remover as credenciais de rede do PDW, use o procedimento armazenado [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) .  
  
Para listar todas as credenciais de rede armazenadas no SQL Server PDW, use a exibição de gerenciamento dinâmico [Sys. dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) .  
  
### <a name="secure-communications"></a>Comunicações seguras  
  
As operações no servidor de carregamento podem usar um caminho UNC para efetuar pull de dados de fora da rede interna confiável. Um invasor na rede ou com a capacidade de influenciar a resolução de nomes pode interceptar ou modificar os dados enviados para o PDW. Isso apresenta um risco de violação e divulgação de informações. Para ajudar a reduzir o risco de adulteração:

- Exigir assinatura na conexão. 
- No servidor de carregamento, defina a seguinte opção de política de grupo em segurança \ Opções de instalação: cliente de rede da Microsoft: assinar digitalmente as comunicações (sempre): habilitada.  
  
## <a name="see-also"></a>Consulte Também  
[Backup e restauração](backup-and-restore-overview.md)  
  
