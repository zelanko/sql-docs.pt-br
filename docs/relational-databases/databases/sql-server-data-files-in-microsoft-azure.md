---
title: Arquivos de dados do SQL Server no Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 10/02/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: d70ab69a1779e19c66fadb1044e0fc6af38a4129
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-data-files-in-microsoft-azure"></a>Arquivos de dados do SQL Server no Microsoft Azure
  ![Arquivos de dados no Azure](../../relational-databases/databases/media/data-files-on-azure.png "Arquivos de dados no Azure")  
  
 Arquivos de dados do SQL Server no Microsoft Azure permitem o suporte nativo para os arquivos de banco de dados do SQL Server armazenados como Blobs do Microsoft Azure. Ele permite que você crie um banco de dados do SQL Server executado localmente ou em uma máquina virtual no Microsoft Azure com um local de armazenamento dedicado a seus dados no Armazenamento de Blobs do Microsoft Azure. Esse aprimoramento simplifica especialmente a movimentação de bancos de dados entre computadores usando operações de anexação e desanexação. Além disso, ele fornece um local de armazenamento alternativo para os arquivos de backup de banco de dados ao permitir que você restaure de ou para o Armazenamento do Microsoft Azure. Em virtude disso, ele permite várias soluções híbridas ao fornecer vários benefícios para virtualização de dados, movimentação de dados, segurança e disponibilidade, baixo custo e facilidade de manutenção, o que proporciona alta disponibilidade e dimensionamento elástico.
 
> [!IMPORTANT]  
>  O armazenamento de bancos de dados do sistema no armazenamento de blobs do Azure não é recomendado e não tem suporte. 

  
 Este tópico apresenta os conceitos e as considerações que são essenciais para armazenar arquivos de dados do SQL Server no serviço de Armazenamento do Microsoft Azure.  
  
 Para ter uma experiência prática sobre como usar esse novo recurso, consulte [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016 ](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
## <a name="why-use-sql-server-data-files-in-microsoft-azure"></a>Por que usar arquivos de dados do SQL Server no Microsoft Azure? 
  
-   **Benefícios da migração fácil e rápida:** esse recurso simplifica o processo de migração movendo um banco de dados de cada vez entre computadores locais, e também entre ambientes locais e de nuvem, sem nenhuma alteração do aplicativo. Em virtude disso, ele oferece suporte a uma migração incremental, preservando sua infraestrutura existente local. Além disso, ter acesso a um armazenamento de dados centralizado simplifica a lógica do aplicativo quando um aplicativo precisa ser executado em vários locais em um ambiente local. Em alguns casos, pode ser necessário configurar rapidamente os centros de computação em locais dispersos geograficamente, que coletam dados de várias origens diferentes. Ao usar esse novo aprimoramento, em vez de mover dados de um local para outro, você poderá armazenar muitos bancos de dados como blobs do Microsoft Azure e, em seguida, executar scripts Transact-SQL para criar bancos de dados em computadores locais ou máquinas virtuais.  
  
-   **Benefícios de custos e armazenamento ilimitado:** este recurso permite ter armazenamento ilimitado fora do site no Microsoft Azure aproveitando os recursos de computação locais. Quando você usa o Microsoft Azure como um local de armazenamento, pode facilmente se concentrar na lógica do aplicativo sem a sobrecarga do gerenciamento de hardware. Se você perder um nó de computação no local, poderá configurar um novo sem nenhuma movimentação de dados.  
  
-   **Benefícios de alta disponibilidade e recuperação de desastres:** usar o recurso de arquivos de dados do SQL Server no Microsoft Azure pode simplificar as soluções de alta disponibilidade e recuperação de desastres. Por exemplo, se uma máquina virtual no Microsoft Azure ou em uma instância do SQL Server falhar, você poderá recriar seus bancos de dados em uma nova instância do SQL Server apenas restabelecendo links para os Blobs do Microsoft Azure.  
  
-   **Benefícios de segurança:** esse novo aprimoramento permite que você separe uma instância de computação de uma instância de armazenamento. Você pode ter um banco de dados totalmente criptografado com a descriptografia ocorrendo apenas na instância de computação, mas não em uma instância de armazenamento. Ou seja, com esse novo aprimoramento, você poderá criptografar todos os dados na nuvem pública usando certificados de TDE (Criptografia de Dados Transparente), que são separados fisicamente dos dados. As chaves de TDE podem ser armazenadas no banco de dados mestre, que é armazenado localmente em seu computador local seguro fisicamente e com backup feito localmente. Você pode usar essas chaves locais para criptografar os dados, que residem no Armazenamento do Microsoft Azure. Se suas credenciais de conta de armazenamento de nuvem forem roubadas, seus dados permanecerão seguros porque os certificados de TDE sempre residirão no local.  
  
-   **Backup de instantâneo:**  Este recurso permite usar os instantâneos do Azure para fornecer backups quase imediatos e restaurações mais rápidas para os arquivos de banco de dados armazenados usando o serviço de Armazenamento de Blobs do Azure. Esse recurso permite que você simplifique as políticas de backup e restauração. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="concepts-and-requirements"></a>Conceitos e requisitos  
  
### <a name="azure-storage-concepts"></a>Conceitos de Armazenamento do Azure  
 Ao usar o recurso de arquivos de dados do SQL Server no Windows Azure, você precisará criar uma conta de armazenamento e um contêiner no Windows Azure. Em seguida, você precisará criar uma credencial do SQL Server, que inclui as informações sobre a política do contêiner, assim como uma assinatura de acesso compartilhado que é necessária para acessar o contêiner.  
  
 No [Microsoft Azure](https://azure.microsoft.com), uma conta de [armazenamento do Azure](https://azure.microsoft.com/services/storage/) representa o nível mais alto do namespace para acesso aos Blobs. Uma conta de armazenamento pode conter um número ilimitado de contêineres, contanto que o seu tamanho total esteja abaixo dos limites de armazenamento. Para obter as informações mais recentes sobre os limites de armazenamento, consulte [Assinatura e limites de serviço, cotas e restrições do Azure](http://docs.microsoft.com/azure/azure-subscription-service-limits). Um contêiner fornece um agrupamento de um conjunto de [Blobs](http://docs.microsoft.com/azure/storage/common/storage-introduction#blob-storage). Todos os blobs devem estar em um contêiner. Uma conta pode conter um número ilimitado de contêineres. Da mesma maneira, um contêiner também pode armazenar um número ilimitado de blobs. Há dois tipos de blobs que podem ser armazenados no Armazenamento do Azure: blobs de blocos e de páginas. Esse novo recurso usa blobs de página, que são mais eficientes quando os intervalos de bytes em um arquivo, são alterados com frequência. Você pode acessar blobs usando o seguinte formato de URL: `http://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="azure-billing-considerations"></a>Considerações sobre cobrança do Azure  
 Estimar o custo do uso dos Serviços do Azure é uma questão importante do processo de tomada de decisão e planejamento. Ao armazenar arquivos de dados do SQL Server no Armazenamento do Azure, você precisa pagar os custos associados ao armazenamento e às transações. Além disso, a implementação do recurso Arquivos de Dados do SQL Server no Armazenamento do Azure exige uma renovação da concessão de Blob em intervalos de 45 a 60 segundos implicitamente. Isso também resulta em custo de transações por arquivo de banco de dados, como arquivos .mdf e .ldf. Use as informações na página [Preços do Azure](http://azure.microsoft.com/pricing/) para ajudar a estimar os custos mensais associados ao uso do Armazenamento do Azure e das Máquinas Virtuais do Azure.  
  
### <a name="sql-server-concepts"></a>Conceitos do SQL Server  
 Ao usar esse novo aprimoramento, você deverá fazer o seguinte:  
  
-   Criar uma política em um contêiner e gerar uma chave SAS (assinatura de acesso compartilhado).  
  
-   Para cada contêiner usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner.  
  
-   É necessário armazenar as informações relacionadas ao contêiner do Armazenamento do Azure, seu nome de política associado e a chave SAS no repositório de credenciais do SQL Server.  
  
 O exemplo a seguir supõe que um contêiner de Armazenamento do Azure tenha sido criado e uma política tenha sido criada com direitos de leitura, gravação, lista. Criar uma política em um contêiner gera uma chave de SAS que pode ser mantida não criptografada na memória e usada pelo SQL Server para acessar os arquivos de blob no contêiner. No trecho de código a seguir, substitua `'<your SAS key>'` por uma entrada semelhante à seguinte: `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`. Para saber mais, confira [Gerenciar o acesso aos recursos de Armazenamento do Azure](http://docs.microsoft.com/azure/storage/blobs/storage-manage-access-to-resources).  
  
```sql
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = '<your SAS key>'  
  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
```  
  
 **Observação importante:** se houver alguma referência ativa aos arquivos de dados em um contêiner, as tentativas de excluir as credenciais correspondentes do SQL Server apresentarão falha.  
  
### <a name="security"></a>Segurança  
 Veja abaixo os requisitos e as considerações sobre segurança ao armazenar os Arquivos de Dados do SQL Server no Armazenamento do Azure.  
  
-   Ao criar um contêiner para o serviço de armazenamento de Blobs do Azure, recomendamos que você defina o acesso como privado. Quando você define o acesso como privado, o contêiner e os dados de blob podem ser lidos somente pelo proprietário da conta do Azure.  
  
-   Ao armazenar arquivos de banco de dados do SQL Server no Armazenamento do Azure, você precisará usar uma assinatura de acesso compartilhado, um URI que concede direitos de acesso restrito a contêineres, blobs, filas e tabelas. Ao usar uma assinatura de acesso compartilhado, você poderá habilitar o SQL Server a acessar recursos em sua conta de armazenamento sem compartilhar a chave de conta de armazenamento do Azure.  
  
-   Além disso, recomendamos que você continue a implementar as práticas tradicionais de segurança locais para seus bancos de dados.  
  
### <a name="installation-prerequisites"></a>Pré-requisitos para instalação  
 Veja abaixo os pré-requisitos de instalação ao armazenar Arquivos de Dados do SQL Server no Azure.  
  
-   **SQL Server local:** SQL Server 2016 e posteriores incluem esse recurso. Para saber como baixar a versão mais recente do SQL Server, consulte [SQL Server](http://www.microsoft.com/sql-server/sql-server-downloads).  
  
-   SQL Server em execução em uma máquina virtual do Azure: se você estiver instalando o [SQL Server em uma Máquina Virtual do Azure](http://azuremarketplace.microsoft.com/marketplace/apps?search=sql%20server&page=1), instale o SQL Server 2016 ou atualize a instância existente. Da mesma forma, você também pode criar uma nova máquina virtual no Azure usando a imagem da plataforma do SQL Server 2016.

  
###  <a name="bkmk_Limitations"></a> Limitações  
  
-   Na versão atual desse recurso, não há suporte para armazenamento de dados do **Fluxo de arquivos** no Armazenamento do Azure. Você pode armazenar dados do **Fluxo de arquivos** em um banco de dados local integrado do armazenamento do Azure, mas não pode mover dados do Fluxo de arquivos entre computadores que usam o Armazenamento do Azure. Para os dados do **FileStream** , recomendamos que você continue usando as técnicas tradicionais para mover os arquivos (.mdf, .ldf) associados ao Filestream entre computadores diferentes.  
  
-   Atualmente, essa nova melhoria não dá suporte a mais de uma instância do SQL Server que acessa os mesmos arquivos de banco de dados no Armazenamento do Azure ao mesmo tempo. Se o Servidor A estiver online com um arquivo de banco de dados ativo e o Servidor B for iniciado por acidente, e também tiver um banco de dados que aponta para o mesmo arquivo de dados, o segundo servidor não iniciará o banco de dados com um código de erro **5120 Não é possível abrir o arquivo físico "%.\*ls". Erro no sistema operacional %d: "%ls"**.  
  
-   Apenas arquivos .mdf, .ldf e .ndf podem ser armazenados no Armazenamento do Azure usando o recurso Arquivos de Dados do SQL Server no Azure.  
  
-   Ao usar o recurso Arquivos de Dados do SQL Server no Azure, não haverá suporte para a replicação geográfica em sua conta de armazenamento. Se uma conta de armazenamento for replicada geograficamente e um failover geográfico acontecer, poderá haver corrupção de banco de dados.  
  
-   Para limitações de capacidade, consulte [Introdução ao armazenamento de Blobs](http://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).  
  
-   Não é possível armazenar dados OLTP in-memory no Blob do Azure usando o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure. Isso ocorre porque o OLTP in-memory tem uma dependência do **Fluxo de arquivos** e, na versão atual desse recurso, não há suporte para armazenamento de dados do **Fluxo de arquivos** no Armazenamento do Azure.  
  
-   Ao usar o recurso Arquivos de Dados do SQL Server no Azure, o SQL Server executa todas as comparações de URL ou de caminho de arquivo usando o Agrupamento definido no banco de dados **mestre** .  
  
-   Os **grupos de disponibilidade AlwaysOn** têm suporte contanto que você não adicione novos arquivos de banco de dados ao banco de dados primário. Se uma operação de banco de dados exigir que um novo arquivo seja criado no banco de dados primário, primeiro desabilite os grupos de disponibilidade AlwaysOn no nó secundário. Em seguida, execute a operação de banco de dados no banco de dados primário e faça o backup do banco de dados no nó primário. Em seguida, restaure o banco de dados para o nó secundário e habilite os grupos de disponibilidade AlwaysOn no nó secundário. Observe que não há suporte para as instâncias de cluster de failover AlwaysOn ao usar o recurso Arquivos de dados do SQL Server no Azure.  
  
-   Durante a operação normal, o SQL Server usa concessões temporárias para reservar os blobs para armazenamento com uma renovação de cada concessão de blob a cada 45 a 60 segundos. Se um servidor falhar e outra instância do SQL Server configurada para usar os mesmos blobs tiver sido iniciada, a nova instância aguardará até 60 segundos pela concessão existente expirar no blob. Se você quiser anexar o banco de dados a outra instância e não puder aguardar a concessão expirar dentro de 60 segundos, interrompa explicitamente a concessão no blob para evitar falhas em operações de anexação.  
  
## <a name="tools-and-programming-reference-support"></a>Suporte a ferramentas e referência de programação  
 Esta seção descreve as ferramentas e as bibliotecas de referência de programação que podem ser usadas ao armazenar arquivos de dados do SQL Server no Armazenamento do Azure.  
  
### <a name="powershell-support"></a>Suporte ao PowerShell  
 Use cmdlets do PowerShell para armazenar arquivos de dados do SQL Server no serviço de Armazenamento de Blobs do Azure, fazendo referência a um caminho de URL do Armazenamento de Blobs, em vez de um caminho do arquivo. Acessar blobs usando o formato de URL a seguir: `http://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="sql-server-object-and-performance-counters-support"></a>Suporte ao objeto SQL Server e aos contadores de desempenho  
 A partir do SQL Server 2014, um novo objeto SQL Server foi adicionado para ser usado com o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure. O novo objeto SQL Server é chamado de [SQL Server, HTTP_STORAGE_OBJECT](../../relational-databases/performance-monitor/sql-server-http-storage-object.md) e pode ser usado pelo Monitor do Sistema para monitorar a atividade ao executar o SQL Server com o Armazenamento do Microsoft Azure.  
  
### <a name="sql-server-management-studio-support"></a>Suporte ao SQL Server Management Studio  
 O SQL Server Management Studio permite usar esse recurso por meio de várias janelas da caixa de diálogo. Por exemplo, você pode digitar o caminho da URL do contêiner de armazenamento, como > https://teststorageaccnt.blob.core.windows.net/testcontainer/:
 
 como um **Caminho** em várias janelas de diálogo, como **Novo Banco de Dados**, **Anexar Banco de Dados**e **Restaurar Banco de Dados**. Para obter mais informações, consulte [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
### <a name="sql-server-management-objects-smo-support"></a>Suporte ao SMO (SQL Server Management Objects)  
 Ao usar o recurso Arquivos de Dados do SQL Server no Azure, há suporte para o SMO (SQL Server Management Objects). Se um objeto SMO exigir um caminho de arquivo, use o formato de URL do BLOB em vez do caminho de um arquivo local, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Para obter mais informações sobre SQL SMO (Server Management Objects), consulte [Guia de Programação do SQL SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) nos Manuais Online do SQL Server.  
  
### <a name="transact-sql-support"></a>Suporte a Transact-SQL  
 Esse novo recurso introduziu a seguinte alteração na área de superfície do Transact-SQL:  
  
-   Uma nova coluna **int** , **credential_id**, na exibição do sistema **sys.master_files** . A coluna **credential_id** é usada para habilitar arquivos de dados habilitados para o Armazenamento do Azure para a referência cruzada a sys.credentials das credenciais criadas para eles. Você pode usá-la para solucionar problemas, como, por exemplo, uma credencial que não pode ser excluída quando há um arquivo de banco de dados que a utiliza.  
  
##  <a name="bkmk_Troubleshooting"></a> Solução de problemas de Arquivos de Dados do SQL Server no Microsoft Azure  
 Para evitar erros devido a recursos sem suporte ou limitações, primeiro analise [Limitations](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations).  
  
 Veja abaixo a lista de erros que você pode obter ao usar o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure.  
  
 **Erros de autenticação**  
  
-   *Não é possível remover a credencial “%.\*ls”, pois ela é usada por um arquivo de banco de dados ativo.*   
    Resolução: você poderá ver este erro ao tentar remover uma credencial que ainda está sendo usada por um arquivo de banco de dados ativo no Armazenamento do Azure. Para descartar a credencial, primeiro exclua o blob associado que contém esse arquivo de banco de dados. Para excluir um blob que tem uma concessão ativa, primeiro você deve interromper a concessão.  
  
-   *A assinatura de acesso compartilhado não foi criada no contêiner corretamente.*   
     Resolução: verifique se você criou uma assinatura de acesso compartilhado no contêiner corretamente. Examine as instruções fornecidas na Lição 2 no [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016 ](../lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md).  
  
-   *A credencial do SQL Server não foi criada corretamente.*   
    Resolução: verifique se você usou "Assinatura de Acesso Compartilhado" para o campo **Identidade** e se criou um segredo corretamente. Examine as instruções fornecidas na Lição 3 no [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016](../lesson-3-database-backup-to-url.md).  
  
 **Erros de blob de concessão:**  
  
-   Erro ao tentar iniciar o SQL Server depois da falha de outra instância usando os mesmos arquivos de blob. Resolução: durante a operação normal, o SQL Server usa concessões temporárias para reservar os blobs para armazenamento com uma renovação de cada concessão de blob a cada 45 a 60 segundos. Se um servidor falhar e outra instância do SQL Server configurada para usar os mesmos blobs tiver sido iniciada, a nova instância aguardará até 60 segundos pela concessão existente expirar no blob. Se você quiser anexar o banco de dados a outra instância e não puder aguardar a concessão expirar dentro de 60 segundos, interrompa explicitamente a concessão no blob para evitar falhas em operações de anexação.  
  
 **Erros de banco de dados**  
  
1.  *Erros ao criar um banco de dados*   
    Resolução: examine as instruções fornecidas na Lição 4 no [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016](../lesson-4-restore-database-to-virtual-machine-from-url.md).  
  
2.  *Erros ao executar a instrução Alter*   
    Resolução: execute a instrução Alter Database mudar quando o banco de dados estiver online. Ao copiar os arquivos de dados no Armazenamento do Azure, sempre crie um blob de páginas, não um blob de blocos. Caso contrário, ALTER Database falhará. Examine as instruções fornecidas na Lição 7 no [Tutorial: Usando o serviço de armazenamento de Blobs do Microsoft Azure com bancos de dados SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
3.  *Código de erro 5120 Não é possível abrir o arquivo físico “%.\*ls”. Erro no sistema operacional %d: “%ls”*   
    Resolução: atualmente, essa nova melhoria não dá suporte a mais de uma instância do SQL Server que acessa os mesmos arquivos de banco de dados no Armazenamento do Azure ao mesmo tempo. Se o Servidor A estiver online com um arquivo de banco de dados ativo e o Servidor B for iniciado por acidente, e também tiver um banco de dados que aponta para o mesmo arquivo de dados, o segundo servidor não iniciará o banco de dados com um código de erro *5120 Não é possível abrir o arquivo físico "%.\*ls". Erro no sistema operacional %d: "%ls"*.  
  
     Para resolver esse problema, primeiro determine se você precisa que o ServerA acesse o arquivo de banco de dados no Armazenamento do Azure. Se não precisar, basta remover as conexões entre o ServerA e os arquivos de banco de dados no Armazenamento do Azure. Para fazer isso, siga estas etapas:  
  
    1.  Defina o caminho do arquivo do Servidor A para uma pasta local usando a instrução ALTER Database.  
  
    2.  Defina o banco de dados como offline no Servidor A.  
  
    3.  Em seguida, copie os arquivos de banco de dados do Armazenamento do Azure para a pasta local no Servidor A. Isso garante que o ServerA ainda terá uma cópia do banco de dados localmente.  
  
    4.  Defina o banco de dados como online.  

## <a name="next-steps"></a>Próximas etapas  
  
[Criar um banco de dados](create-a-database.md)