---
title: Arquivos de dados do SQL Server no Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 12/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ba61e7cc35d9cd0a0f63e3e2f89980b12c6904d5
ms.sourcegitcommit: 26868c8ac3217176b370d972a26d307598a10328
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2019
ms.locfileid: "74833577"
---
# <a name="sql-server-data-files-in-microsoft-azure"></a>Arquivos de dados do SQL Server no Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ![Arquivos de dados no Azure](../../relational-databases/databases/media/data-files-on-azure.png "Daarquivos ta no Azure ")  
  
Arquivos de dados do SQL Server no Microsoft Azure permitem o suporte nativo para os arquivos de banco de dados do SQL Server armazenados como blobs. Ele permite que você crie um banco de dados do SQL Server executado localmente ou em uma máquina virtual no Microsoft Azure com um local de armazenamento dedicado a seus dados no armazenamento de Blobs do Microsoft Azure. Ele também simplifica o processo de movimentação de bancos de dados entre computadores. Você pode desanexar bancos de dados de um computador e anexá-los a outro computador. Além disso, ele fornece um local de armazenamento alternativo para os arquivos de backup de banco de dados ao permitir que você restaure de ou para o Armazenamento do Microsoft Azure. Em virtude disso, ele permite várias soluções híbridas ao fornecer vários benefícios para virtualização de dados, movimentação de dados, segurança e disponibilidade, baixo custo e facilidade de manutenção, o que proporciona alta disponibilidade e dimensionamento elástico.
 
> [!IMPORTANT]  
>  O armazenamento de bancos de dados do sistema no armazenamento de blobs do Azure não é recomendado e não tem suporte. 

 Este tópico apresenta os conceitos e as considerações que são essenciais para armazenar arquivos de dados do SQL Server no serviço de Armazenamento do Microsoft Azure.  
  
 Para uma experiência prática sobre como usar esse novo recurso, consulte [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
## <a name="why-use-sql-server-data-files-in-microsoft-azure"></a>Por que usar arquivos de dados do SQL Server no Microsoft Azure? 

- **Benefícios da migração fácil e rápida:** esse recurso simplifica o processo de migração movendo um banco de dados de cada vez entre computadores locais e também entre ambientes locais e de nuvem, sem nenhuma alteração de aplicativo. Em virtude disso, ele oferece suporte a uma migração incremental, preservando sua infraestrutura existente local. Além disso, ter acesso a um armazenamento de dados centralizado simplifica a lógica do aplicativo quando um aplicativo precisa ser executado em vários locais em um ambiente local. Em alguns casos, pode ser necessário configurar rapidamente os centros de computação em locais dispersos geograficamente, que coletam dados de várias origens diferentes. Ao usar esse novo aprimoramento, em vez de mover dados de um local para outro, você poderá armazenar muitos bancos de dados como blobs do Microsoft Azure e, em seguida, executar scripts Transact-SQL para criar bancos de dados em computadores locais ou máquinas virtuais.

- **Benefícios de custos e armazenamento ilimitados:** este recurso permite ter armazenamento ilimitado fora do local no Microsoft Azure, aproveitando os recursos de computação locais. Quando você usa o Microsoft Azure como um local de armazenamento, pode facilmente se concentrar na lógica do aplicativo sem a sobrecarga do gerenciamento de hardware. Se você perder um nó de computação no local, poderá configurar um novo sem nenhuma movimentação de dados.

- **Benefícios de alta disponibilidade e recuperação de desastres:** usar o recurso de arquivos de dados do SQL Server no Microsoft Azure pode simplificar as soluções de alta disponibilidade e recuperação de desastres. Por exemplo, se uma máquina virtual no Microsoft Azure ou em uma instância do SQL Server falhar, você poderá recriar seus bancos de dados em uma nova instância do SQL Server apenas restabelecendo links para os blobs.

- **Benefícios de segurança:** esse novo aprimoramento permite que você separe uma instância de computação de uma instância de armazenamento. Você pode ter um banco de dados totalmente criptografado com a descriptografia ocorrendo apenas na instância de computação, mas não em uma instância de armazenamento. Ou seja, com esse novo aprimoramento, você poderá criptografar todos os dados na nuvem pública usando certificados de TDE (Criptografia de Dados Transparente), que são separados fisicamente dos dados. As chaves de TDE podem ser armazenadas no banco de dados mestre, que é armazenado localmente em seu computador local seguro fisicamente e com backup feito localmente. Você pode usar essas chaves locais para criptografar os dados, que residem no Armazenamento do Microsoft Azure. Se suas credenciais de conta de armazenamento de nuvem forem roubadas, seus dados permanecerão seguros porque os certificados de TDE sempre residirão no local.

- **Backup de instantâneo:**  este recurso permite usar os instantâneos do Azure para fornecer backups quase imediatos e restaurações mais rápidas para os arquivos de banco de dados armazenados usando o serviço de Armazenamento de Blobs do Azure. Essa funcionalidade permite simplificar suas políticas de backup e restauração. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  

## <a name="concepts-and-requirements"></a>Conceitos e requisitos  
  
Os discos do Azure são compatíveis com soluções de continuidade dos negócios e recuperação de desastres em toda a empresa. Se você armazenar seus bancos de dados diretamente em blobs ou nos arquivos premium do Azure, eles não serão associados automaticamente à sua VM para infraestrutura, gerenciamento e monitoramento.

Colocar os arquivos de banco de dados em blobs de páginas é um recurso mais avançado do que usar discos do Azure, que são simples e amigáveis ao usuário.

A diretriz básica é usar discos do Azure, a menos que você tenha um cenário em que realmente precise evitar a criação de uma cópia dos dados para backups ou a restauração como uma operação de tamanho de dados. Para alta disponibilidade e recuperação de desastres, o uso de backup regular para URL ou backup gerenciado para o armazenamento de blobs também é muito mais útil do que os backups de instantâneo de arquivo, pois você obtém gerenciamento de ciclo de vida, suporte a várias regiões, exclusão reversível e todos os outros recursos do armazenamento de blobs de seus backups.

### <a name="azure-storage-concepts"></a>Conceitos de Armazenamento do Azure  
Ao usar o recurso de arquivos de dados do SQL Server no Azure, você precisará criar um contêiner e uma conta de armazenamento no Azure. Em seguida, você precisará criar uma credencial do SQL Server, que inclui as informações sobre a política do contêiner, assim como uma assinatura de acesso compartilhado que é necessária para acessar o contêiner.  

No [Microsoft Azure](https://azure.microsoft.com), uma conta de [armazenamento do Azure](https://azure.microsoft.com/services/storage/) representa o nível mais alto do namespace para acesso aos blobs. Uma conta de armazenamento pode conter um número ilimitado de contêineres, contanto que o seu tamanho total esteja abaixo dos limites de armazenamento. Para obter as informações mais recentes sobre os limites de armazenamento, consulte [Assinatura e limites de serviço, cotas e restrições do Azure](https://docs.microsoft.com/azure/azure-subscription-service-limits). Um contêiner fornece um agrupamento de conjunto de [blobs](https://docs.microsoft.com/azure/storage/common/storage-introduction#blob-storage). Todos os blobs devem estar em um contêiner. Uma conta pode conter um número ilimitado de contêineres. Da mesma maneira, um contêiner pode armazenar um número ilimitado de blobs. Há dois tipos de blobs que podem ser armazenados no Armazenamento do Azure: blobs de blocos e de páginas. Esse novo recurso usa blobs de página, que são mais eficientes quando os intervalos de bytes em um arquivo, são alterados com frequência. Você pode acessar blobs usando o seguinte formato de URL: `https://storageaccount.blob.core.windows.net/<container>/<blob>`.  

### <a name="azure-billing-considerations"></a>Considerações sobre cobrança do Azure  

 Estimar o custo do uso dos Serviços do Azure é uma questão importante do processo de tomada de decisão e planejamento. Ao armazenar arquivos de dados do SQL Server no Armazenamento do Azure, você precisa pagar os custos associados ao armazenamento e às transações. Além disso, a implementação do recurso Arquivos de Dados do SQL Server no Armazenamento do Azure exige uma renovação da concessão de Blob em intervalos de 45 a 60 segundos implicitamente. Isso também resulta em custo de transações por arquivo de banco de dados, como arquivos .mdf e .ldf. Use as informações na página [Preços do Azure](https://azure.microsoft.com/pricing/) para ajudar a estimar os custos mensais associados ao uso do Armazenamento do Azure e das Máquinas Virtuais do Azure.  
  
### <a name="sql-server-concepts"></a>Conceitos do SQL Server  

Ao usar esse novo aprimoramento, você deverá fazer o seguinte:

- Crie uma política em um contêiner e gere uma chave SAS (assinatura de acesso compartilhado).

- Para cada contêiner usado por um arquivo de log ou de dados, crie uma credencial do SQL Server cujo nome corresponda ao caminho do contêiner.

- Armazene as informações relacionadas ao contêiner do Armazenamento do Azure, seu nome de política associado e a chave SAS no repositório de credenciais do SQL Server.

O exemplo a seguir supõe que um contêiner de Armazenamento do Azure tenha sido criado e uma política tenha sido criada com direitos de leitura, gravação e lista. Criar uma política em um contêiner gera uma chave de SAS, que pode ser mantida não criptografada na memória e usada pelo SQL Server para acessar os arquivos de blob no contêiner. 

No snippet de código a seguir, substitua `'<your SAS key>'` pela chave SAS. A chave SAS será parecida com `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`.

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

>[!IMPORTANT]
>se houver alguma referência ativa aos arquivos de dados em um contêiner, as tentativas de excluir as credenciais correspondentes do SQL Server apresentarão falha.

Para saber mais, confira [Gerenciar o acesso aos recursos de Armazenamento do Azure](https://docs.microsoft.com/azure/storage/blobs/storage-manage-access-to-resources).  

### <a name="security"></a>Segurança  
 Veja abaixo os requisitos e as considerações sobre segurança ao armazenar os Arquivos de Dados do SQL Server no Armazenamento do Azure.

- Ao criar um contêiner para o serviço de armazenamento de Blobs do Azure, recomendamos que você defina o acesso como privado. Quando você define o acesso como privado, o contêiner e os dados de blob podem ser lidos somente pelo proprietário da conta do Azure.

- Ao armazenar arquivos de banco de dados do SQL Server no Armazenamento do Azure, você precisará usar uma assinatura de acesso compartilhado, um URI que concede direitos de acesso restrito a contêineres, blobs, filas e tabelas. Ao usar uma assinatura de acesso compartilhado, você poderá habilitar o SQL Server a acessar recursos em sua conta de armazenamento sem compartilhar a chave de conta de armazenamento do Azure.

- Além disso, recomendamos que você continue a implementar as práticas tradicionais de segurança locais para seus bancos de dados.  
  
### <a name="installation-prerequisites"></a>Pré-requisitos da instalação  
 Veja abaixo os pré-requisitos de instalação ao armazenar Arquivos de Dados do SQL Server no Azure.

- **SQL Server local:** o SQL Server 2016 e posteriores incluem esse recurso. Para saber como baixar a versão mais recente do SQL Server, consulte [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads).

- Execução do SQL Server em uma máquina virtual do Azure: se você estiver instalando o [SQL Server em uma máquina virtual do Azure](https://azuremarketplace.microsoft.com/marketplace/apps?search=sql%20server&page=1), instale o SQL Server 2016 ou atualize a instância existente. Da mesma forma, você também pode criar uma nova máquina virtual no Azure usando a imagem da plataforma do SQL Server 2016.

  
###  <a name="bkmk_Limitations"></a> Limitações  
  
- Na versão atual desse recurso, não há suporte para armazenamento de dados do **Fluxo de arquivos** no Armazenamento do Azure. Você pode armazenar dados de **FileStream** em um banco de dados que também contém arquivos de dados armazenados no Armazenamento do Azure, mas todos os arquivos de dados de FileStream devem ser armazenados no armazenamento local.  Como os dados de FileStream precisam residir no armazenamento local, eles não podem ser movidos entre computadores usando o Armazenamento do Azure, portanto, é recomendável que você continue usando [técnicas tradicionais](../../relational-databases/blob/move-a-filestream-enabled-database.md) para mover os dados associados ao FileStream entre computadores diferentes.  
  
- Atualmente, essa nova melhoria não dá suporte a mais de uma instância do SQL Server que acessa os mesmos arquivos de banco de dados no Armazenamento do Azure ao mesmo tempo. Se o Servidor A estiver online com um arquivo de banco de dados ativo e o Servidor B for iniciado por acidente e também tiver um banco de dados que aponta para o mesmo arquivo de dados, o segundo servidor não iniciará o banco de dados com um código de erro **5120 Não é possível abrir o arquivo físico "%.\*ls". Erro no sistema operacional %d: "%ls"** .  
  
- Apenas arquivos .mdf, .ldf e .ndf podem ser armazenados no Armazenamento do Azure usando o recurso Arquivos de Dados do SQL Server no Azure.  
  
- Ao usar o recurso Arquivos de Dados do SQL Server no Azure, não haverá suporte para a replicação geográfica em sua conta de armazenamento. Se uma conta de armazenamento for replicada geograficamente e um failover geográfico acontecer, poderá haver corrupção de banco de dados.  
  
- Para limitações de capacidade, consulte [Introdução ao armazenamento de Blobs](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).  
  
- Não é possível armazenar dados OLTP in-memory no armazenamento de Blobs usando o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure. Isso ocorre porque o OLTP in-memory tem uma dependência do **Fluxo de arquivos** e, na versão atual desse recurso, não há suporte para armazenamento de dados do **Fluxo de arquivos** no Armazenamento do Azure.  
  
- Ao usar o recurso Arquivos de Dados do SQL Server no Azure, o SQL Server executa todas as comparações de URL ou de caminho de arquivo usando a ordenação definida no banco de dados **mestre**.  
  
- Os **grupos de disponibilidade AlwaysOn** têm suporte contanto que você não adicione novos arquivos de banco de dados ao banco de dados primário. Se uma operação de banco de dados exigir que um novo arquivo seja criado no banco de dados primário, primeiro desabilite os grupos de disponibilidade no nó secundário. Em seguida, execute a operação de banco de dados no banco de dados primário e faça o backup do banco de dados no nó primário. Em seguida, restaure o banco de dados para o nó secundário. Depois de concluir, habilite novamente grupos de disponibilidade Always On no nó secundário. 

   >[!NOTE]
   >Não há suporte para as instâncias de cluster de failover Always On ao usar o recurso Arquivos de dados do SQL Server no Azure.
  
- Durante a operação normal, o SQL Server usa concessões temporárias para reservar os blobs para armazenamento com uma renovação de cada concessão de blob a cada 45 a 60 segundos. Se um servidor falhar e outra instância do SQL Server configurada para usar os mesmos blobs tiver sido iniciada, a nova instância aguardará até 60 segundos pela concessão existente expirar no blob. Se você quiser anexar o banco de dados a outra instância e não puder aguardar a concessão expirar dentro de 60 segundos, libere explicitamente a concessão no blob.
  
## <a name="tools-and-programming-reference-support"></a>Suporte a ferramentas e referência de programação  
 Esta seção descreve as ferramentas e as bibliotecas de referência de programação que podem ser usadas ao armazenar arquivos de dados do SQL Server no Armazenamento do Azure.  
  
### <a name="powershell-support"></a>Suporte ao PowerShell  
 Use cmdlets do PowerShell para armazenar arquivos de dados do SQL Server no serviço de armazenamento de Blobs, fazendo referência a um caminho de URL do Armazenamento de Blobs, em vez de um caminho do arquivo. Acessar blobs usando o formato de URL a seguir: `https://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="sql-server-object-and-performance-counters-support"></a>Suporte ao objeto SQL Server e aos contadores de desempenho  
 A partir do SQL Server 2014, um novo objeto SQL Server foi adicionado para ser usado com o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure. O novo objeto SQL Server é chamado de [SQL Server, HTTP_STORAGE_OBJECT](../../relational-databases/performance-monitor/sql-server-http-storage-object.md) e pode ser usado pelo Monitor do Sistema para monitorar a atividade ao executar o SQL Server com o Armazenamento do Microsoft Azure.  
  
### <a name="sql-server-management-studio-support"></a>Suporte ao SQL Server Management Studio  
 O SQL Server Management Studio permite usar esse recurso por meio de várias janelas da caixa de diálogo. Por exemplo, `https://teststorageaccnt.blob.core.windows.net/testcontainer/` representa o caminho da URL de um contêiner de armazenamento.
 
 como um **Caminho** em várias janelas de diálogo, como **Novo Banco de Dados**, **Anexar Banco de Dados**e **Restaurar Banco de Dados**. Para saber mais, confira [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
### <a name="sql-server-management-objects-smo-support"></a>Suporte ao SMO (SQL Server Management Objects)  
 Ao usar o recurso Arquivos de Dados do SQL Server no Azure, há suporte para o SMO (SQL Server Management Objects). Se um objeto SMO exigir um caminho de arquivo, use o formato de URL do BLOB em vez do caminho de um arquivo local, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Para obter mais informações sobre SQL SMO (Server Management Objects), consulte [Guia de Programação do SQL SMO &#40;SQL Server Management Objects&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md) nos Manuais Online do SQL Server.  
  
### <a name="transact-sql-support"></a>Suporte a Transact-SQL  
 Esse novo recurso introduziu a seguinte alteração na área de superfície do Transact-SQL:

- Uma nova coluna **int** , **credential_id**, na exibição do sistema **sys.master_files** . A coluna **credential_id** é usada para habilitar arquivos de dados para o Armazenamento do Azure para a referência cruzada `sys.credentials` das credenciais criadas para eles. Você pode usá-la para solucionar problemas, como, por exemplo, uma credencial que não pode ser excluída quando há um arquivo de banco de dados que a utiliza.  
  
##  <a name="bkmk_Troubleshooting"></a> Solução de problemas de Arquivos de Dados do SQL Server no Microsoft Azure  
 Para evitar erros devido a recursos sem suporte ou limitações, primeiro analise [Limitations](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations).  
  
 Veja abaixo a lista de erros que você pode obter ao usar o recurso Arquivos de Dados do SQL Server no Armazenamento do Azure.  
  
 **Erros de autenticação**  
  
- *Não é possível remover a credencial “%.\*ls”, pois ela é usada por um arquivo de banco de dados ativo.*    
    Resolução: você poderá ver este erro ao tentar remover uma credencial que ainda está sendo usada por um arquivo de banco de dados ativo no Armazenamento do Azure. Para descartar a credencial, primeiro exclua o blob associado que contém esse arquivo de banco de dados. Para excluir um blob que tem uma concessão ativa, primeiro você deve liberar a concessão.  
  
- *A assinatura de acesso compartilhado não foi criada no contêiner corretamente.*    
     Resolução: verifique se você criou uma assinatura de acesso compartilhado no contêiner corretamente. Analise as instruções fornecidas na lição 2 em [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md).  
  
- *A credencial do SQL Server não foi criada corretamente.*    
    Resolução: Verifique se você usou “Assinatura de Acesso Compartilhado” para o campo **Identity** e criou um segredo corretamente. Analise as instruções fornecidas na lição 3 em [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../lesson-3-database-backup-to-url.md).  
  
 **Erros de blob de concessão:**  
  
- Erro ao tentar iniciar o SQL Server depois da falha de outra instância usando os mesmos arquivos de blob. Resolução: Durante a operação normal, o SQL Server usa concessões temporárias para reservar os blobs para armazenamento com uma renovação de cada concessão de blob a cada 45 a 60 segundos. Se um servidor falhar e outra instância do SQL Server configurada para usar os mesmos blobs tiver sido iniciada, a nova instância aguardará até 60 segundos pela concessão existente expirar no blob. Se você quiser anexar o banco de dados a outra instância e não puder aguardar a concessão expirar dentro de 60 segundos, libere explicitamente a concessão no blob para evitar falhas em operações de anexação.  
  
 **Erros de banco de dados**  
  
1.  *Erros ao criar um banco de dados*   
    Resolução: Analise as instruções fornecidas na lição 4 em [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../lesson-4-restore-database-to-virtual-machine-from-url.md).  
  
2.  *Erros ao executar a instrução Alter*   
    Resolução: execute a instrução Alterar Banco de Dados quando o banco de dados estiver online. Ao copiar os arquivos de dados no Armazenamento do Azure, sempre crie um blob de páginas, não um blob de blocos. Caso contrário, ALTER Database falhará. Analise as instruções fornecidas na lição 7 em [Tutorial: usar o serviço de Armazenamento de Blobs do Microsoft Azure com os bancos de dados do SQL Server 2016](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
3.  *Código de erro 5120 Não é possível abrir o arquivo físico “%.\*ls”. Erro no sistema operacional %d: "%ls"*   

    Resolução: Atualmente, essa nova melhoria não dá suporte a mais de uma instância do SQL Server acessando os mesmos arquivos de banco de dados no Armazenamento do Azure ao mesmo tempo. Se o Servidor A estiver online com um arquivo de banco de dados ativo e o Servidor B for iniciado por acidente e também tiver um banco de dados que aponta para o mesmo arquivo de dados, o segundo servidor não iniciará o banco de dados com um código de erro *5120 Não é possível abrir o arquivo físico "%.\*ls". Erro no sistema operacional %d: "%ls"* .  
  
     Para resolver esse problema, primeiro determine se você precisa que o ServerA acesse o arquivo de banco de dados no Armazenamento do Azure. Se não precisar, remova as conexões entre o Servidor A e os arquivos de banco de dados no Armazenamento do Azure. Para fazer isso, siga estas etapas:  
  
    1.  Defina o caminho do arquivo do Servidor A para uma pasta local usando a instrução ALTER Database.  
  
    2.  Defina o banco de dados como offline no Servidor A.  
  
    3.  Em seguida, copie os arquivos de banco de dados do Armazenamento do Azure para a pasta local no Servidor A. Isso garante que o ServerA ainda terá uma cópia do banco de dados localmente.  
  
    4.  Defina o banco de dados como online.  

## <a name="next-steps"></a>Próximas etapas  
  
[Criar um banco de dados](create-a-database.md)
