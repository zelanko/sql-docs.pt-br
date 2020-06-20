---
title: FILESTREAM (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server]
- FILESTREAM [SQL Server], about
- FILESTREAM [SQL Server], overview
ms.assetid: 9a5a8166-bcbe-4680-916c-26276253eafa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 971f45fd69f381a8997bb2f8f08444f4d9c107c4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955396"
---
# <a name="filestream-sql-server"></a>FILESTREAM (SQL Server)
  O FILESTREAM permite que aplicativos baseados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazenem dados não estruturados, como documentos e imagens, no sistema de arquivos. Os aplicativos podem utilizar as APIs de streaming avançado e o desempenho do sistema de arquivos e, ao mesmo tempo, manter consistência transacional entre os dados não estruturados e os dados estruturados correspondentes.  
  
 O FILESTREAM integra o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com um sistema de arquivos NTFS armazenando `varbinary(max)` dados BLOB (objeto binário grande) como arquivos no sistema de arquivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] podem inserir, atualizar, consultar, pesquisar e fazer backup de dados FILESTREAM. As interfaces do sistema de arquivos do Win32 fornecem acesso de streaming aos dados.  
  
 O FILESTREAM usa o cache do sistema NT para armazenar dados de arquivos. Isso ajuda a reduzir qualquer efeito que os dados FILESTREAM possam ter no desempenho do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O pool de buffers do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é usado. Portanto essa memória está disponível para processamento de consulta.  
  
 FILESTREAM não é habilitado automaticamente quando você instalar ou atualiza o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você deve habilitar o FILESTREAM usando o SQL Server Configuration Manager e o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para usar o FILESTREAM, você deve criar ou modificar um banco de dados para conter um tipo especial de grupo de arquivos. Então, crie ou modifique uma tabela de forma que ela contenha uma coluna `varbinary(max)` com o atributo FILESTREAM. Depois que você concluir essas tarefas, poderá usar [!INCLUDE[tsql](../../includes/tsql-md.md)] e Win32 para gerenciar os dados de FILESTREAM.  
  
 Para obter mais informações sobre como instalar e usar FILESTREAM, consulte a lista de [Tarefas relacionadas](#reltasks).  
  
##  <a name="when-to-use-filestream"></a><a name="whentouse"></a>Quando usar FILESTREAM  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os BLOBs podem ser dados `varbinary(max)` padrão que armazenam os dados em tabelas ou objetos `varbinary(max)` FILESTREAM que armazenam os dados no sistema de arquivos. O tamanho e o uso dos dados determinam se você deve usar armazenamento de banco de dados ou armazenamento de sistema de arquivos. Se as condições a seguir forem verdadeiras, você deve considerar o uso de FILESTREAM:  
  
-   Os objetos que estão sendo armazenados têm, em média, mais de 1 MB.  
  
-   O acesso rápido para leitura é importante.  
  
-   Você está desenvolvendo aplicativos que usam uma camada intermediária para lógica de aplicativo.  
  
 Para objetos menores, o armazenamento de BLOBs `varbinary(max)` no banco de dados normalmente fornece melhor desempenho de streaming.  
  
  
##  <a name="filestream-storage"></a><a name="storage"></a>Armazenamento de FILESTREAM  
 O armazenamento de FILESTREAM é implementado como uma coluna `varbinary(max)` na qual os dados são armazenados como BLOBs no sistema de arquivos. Os tamanhos dos BLOBs são limitados apenas pelo tamanho do volume do sistema de arquivos. A limitação padrão de `varbinary(max)` tamanhos de arquivos de 2 GB não se aplica a BLOBs que são armazenados no sistema de arquivos.  
  
 Para determinar que uma coluna deve armazenar dados no sistema de arquivos, especifique o atributo FILESTREAM em uma coluna `varbinary(max)`. Isso faz com que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazene todos os dados dessa coluna no sistema de arquivos, mas não no arquivo do banco de dados.  
  
 Os dados FILESTREAM devem ser armazenados em grupos de arquivos FILESTREAM. Um grupo de arquivos FILESTREAM é um grupo de arquivos especial que contém diretórios do sistema de arquivos em vez dos próprios arquivos. Esses diretórios do sistema de arquivos são chamados de *contêineres de dados*. Os contêineres de dados são a interface entre armazenamento [!INCLUDE[ssDE](../../includes/ssde-md.md)] e armazenamento de sistema de arquivos.  
  
 Ao usar armazenamento de FILESTREAM, considere o seguinte:  
  
-   Quando uma tabela contém uma coluna FILESTREAM, cada linha deve ter uma ID de linha exclusiva não nula.  
  
-   Vários contêineres de dados podem ser adicionados a um grupo de arquivos FILESTREAM.  
  
-   Os contêineres de dados FILESTREAM não podem ser aninhados.  
  
-   Quando você usa clustering de failover, os grupos de arquivos FILESTREAM devem estar em recursos de disco compartilhados.  
  
-   Grupos de arquivos FILESTREAM podem estar em volumes compactados.  
  
### <a name="integrated-management"></a>Gerenciamento integrado  
 Como o FILESTREAM é implementado como uma coluna `varbinary(max)` e integrado diretamente ao [!INCLUDE[ssDE](../../includes/ssde-md.md)], a maioria das funções e ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionam sem nenhuma modificação para dados FILESTREAM. Por exemplo, é possível usar todos os modelos de backup e recuperação com dados FILESTREAM e o backup dos dados FILESTREAM pode ser feito com os dados estruturados no banco de dados. Se você não desejar fazer backup de dados FILESTREAM com dados relacionais, poderá usar um backup parcial para excluir grupos de arquivos FILESTREAM.  

  
### <a name="integrated-security"></a>Segurança Integrada  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados FILESTREAM são protegidos exatamente como outros dados, com a concessão de permissões em níveis de tabela ou coluna. Se um usuário tiver permissão para a coluna FILESTREAM em uma tabela, ele poderá abrir os arquivos associados.  
  
> [!NOTE]  
>  Não há suporte para criptografia em dados FILESTREAM.  
  
 Apenas a conta sob a qual a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executada recebe permissões NTFS para o contêiner FILESTREAM. É recomendável que nenhuma outra conta receba permissões no contêiner de dados.  
  
> [!NOTE]  
>  Os logons do SQL não funcionarão com contêineres FILESTREAM. Somente a autenticação NTFS funcionará com contêineres FILESTREAM.  
  
##  <a name="accessing-blob-data-with-transact-sql-and-file-system-streaming-access"></a><a name="dual"></a> Acessando dados BLOB com o Transact-SQL e o acesso a streaming do sistema de arquivos  
 Depois de armazenar dados em uma coluna FILESTREAM, você pode acessar os arquivos usando transações [!INCLUDE[tsql](../../includes/tsql-md.md)] ou usando APIs do Win32.  
  
### <a name="transact-sql-access"></a>Acesso ao Transact-SQL  
 Usando [!INCLUDE[tsql](../../includes/tsql-md.md)], é possível inserir, atualizar e excluir dados FILESTREAM:  
  
-   Você pode usar uma operação de inserção para pré-popular um campo FILESTREAM com um valor nulo, vazio ou com dados embutidos relativamente curtos. No entanto uma quantidade grande de dados é transmitida de maneira mais eficiente em um arquivo que usa interfaces Win32.  
  
-   Ao atualizar um campo FILESTREAM, você modifica os dados BLOB subjacentes no sistema de arquivos. Quando um campo FILESTREAM é definido como NULL, os dados BLOB associados ao campo são excluídos. Não é possível usar uma atualização de [!INCLUDE[tsql](../../includes/tsql-md.md)] em bloco, implementada como UPDATE **.** Write(), para executar atualizações parciais nos dados.  
  
-   Ao excluir uma linha ou ao excluir ou truncar uma tabela que contém dados FILESTREAM, você também exclui os dados BLOB subjacentes do sistema de arquivos.  
  
### <a name="file-system-streaming-access"></a>Acesso a streaming do sistema de arquivos  
 O suporte a streaming do Win32 funciona no contexto de uma transação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dentro de uma transação, é possível usar funções FILESTREAM para obter um caminho do sistema de arquivos UNC lógico de um arquivo. Em seguida, use a API OpenSqlFilestream para obter um identificador de arquivo. Esse identificador pode então ser usado por interfaces de streaming de arquivo do Win32, como ReadFile() e WriteFile(), para acessar e atualizar o arquivo por meio do sistema de arquivos.  
  
 Como as operações de arquivo são transacionais, não é possível excluir ou renomear arquivos FILESTREAM por meio do sistema de arquivos.  
  
 **Modelo de instrução**  
  
 O acesso ao sistema de arquivos FILESTREAM modela uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] usando abertura e fechamento de arquivo. A instrução inicia quando um identificador de arquivo é aberto e termina quando o identificador é fechado. Por exemplo, quando um identificador de gravação é fechado, qualquer gatilho AFTER que esteja registrado na tabela será acionado como se uma instrução UPDATE fosse concluída.  
  
 **Namespace de armazenamento**  
  
 No FILESTREAM, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] controla o namespace do sistema de arquivos físico do BLOB. Uma nova função intrínseca, [PathName](/sql/relational-databases/system-functions/pathname-transact-sql), fornece o caminho UNC lógico do BLOB que corresponde a cada célula FILESTREAM na tabela. O aplicativo usa esse caminho lógico para obter o identificador do Win32 e operar nos dados BLOB usando interfaces normais de sistema de arquivos do Win32. A função retornará NULL se o valor da coluna FILESTREAM for NULL.  
  
 **Acesso a sistema de arquivos transacionado**  
  
 Uma nova função intrínseca, [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql), fornece o token que representa a transação atual à qual a sessão está associada. A transação deve ter sido iniciada e ainda não anulada ou confirmada. Obtendo um token, o aplicativo associa as operações de streaming do sistema de arquivos FILESTREAM a uma transação iniciada. A função retorna NULL no caso de nenhuma transação explicitamente iniciada.  
  
 Todos os identificadores de arquivo devem ser fechados antes de a transação ser confirmada ou anulada. Se um identificador for deixado aberto além do escopo da transação, leituras adicionais em relação ao identificador provocarão uma falha. Gravações adicionais em relação ao identificador serão bem-sucedidas, mas os dados reais não serão gravados em disco. De maneira semelhante, se o banco de dados ou a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for desligado, todos os identificadores abertos serão invalidados.  
  
 **Durabilidade transacional**  
  
 Com FILESTREAM, na confirmação da transação, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica a durabilidade da transação de dados BLOB FILESTREAM que são modificados no acesso de streaming ao sistema de arquivos.  
  
 **Semântica de isolamento**  
  
 A semântica de isolamento é governada pelos níveis de isolamento da transação do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O nível de isolamento confirmado por leitura tem suporte para [!INCLUDE[tsql](../../includes/tsql-md.md)] e acesso ao sistema de arquivos. As operações de leitura repetidas, assim como os isolamentos de instantâneo e serializáveis, têm suporte. Não há suporte para leitura suja.  
  
 As operações de abertura de acesso ao sistema de arquivos não aguardam nenhum bloqueio. Em vez disso, as operações de abertura falham imediatamente caso não possam acessar os dados por causa do isolamento da transação. As chamadas da API de streaming falharão com ERROR_SHARING_VIOLATION se a operação de abertura não puder continuar por causa de violação de isolamento.  
  
 Para permitir a realização de atualizações parciais, o aplicativo pode emitir um controle de FS de dispositivo (FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT) para buscar o conteúdo antigo no arquivo ao qual o identificador aberto faz referência. Isso acionará uma cópia de conteúdo antigo no lado do servidor. Para obter melhor desempenho do aplicativo e evitar a ocorrência de tempos limites potenciais ao trabalhar com arquivos muito grandes, recomendamos usar E/S assíncrona.  
  
 Se o FSCTL for emitido após o identificador ter sido gravado, a última operação de gravação persistirá e as gravações anteriores feitas no identificador serão perdidas.  
  
 **APIs do sistema de arquivos e níveis de isolamento com suporte**  
  
 Quando uma API do sistema de arquivos não pode abrir um arquivo devido a uma violação de isolamento, uma exceção ERROR_SHARING_VIOLATION é retornada. Essa violação de isolamento ocorre quando duas transações tentam acessar o mesmo arquivo. O resultado da operação de acesso depende do modo no qual o arquivo foi aberto e da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual a transação está sendo executada. A tabela a seguir descreve os possíveis resultados para duas transações que estão acessando o mesmo arquivo.  
  
|Transação 1|Transação 2|Resultado no SQL Server 2008|Resultado no SQL Server 2008 R2 e em versões posteriores|  
|-------------------|-------------------|--------------------------------|------------------------------------------------------|  
|Abrir para leitura.|Abrir para leitura.|Ambas realizadas com êxito.|Ambas realizadas com êxito.|  
|Abrir para leitura.|Abrir para gravação.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam as operações de leitura executadas na transação 1.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam as operações de leitura executadas na transação 1.|  
|Abrir para gravação.|Abrir para leitura.|A abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|Ambas realizadas com êxito.|  
|Abrir para gravação.|Abrir para gravação.|A abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|A abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|  
|Abrir para leitura.|Abrir para SELECT.|Ambas realizadas com êxito.|Ambas realizadas com êxito.|  
|Abrir para leitura.|Abrir para UPDATE ou DELETE.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam as operações de leitura executadas na transação 1.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam as operações de leitura executadas na transação 1.|  
|Abrir para gravação.|Abrir para SELECT.|A transação 2 é bloqueada até a transação 1 confirmar ou finalizar a transação, ou o bloqueio da transação atingir o tempo limite.|Ambas realizadas com êxito.|  
|Abrir para gravação.|Abrir para UPDATE ou DELETE.|A transação 2 é bloqueada até a transação 1 confirmar ou finalizar a transação, ou o bloqueio da transação atingir o tempo limite.|A transação 2 é bloqueada até a transação 1 confirmar ou finalizar a transação, ou o bloqueio da transação atingir o tempo limite.|  
|Abrir para SELECT.|Abrir para leitura.|Ambas realizadas com êxito.|Ambas realizadas com êxito.|  
|Abrir para SELECT.|Abrir para gravação.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam a transação 1.|Ambas realizadas com êxito. As operações de gravação na transação 2 não afetam a transação 1.|  
|Abrir para UPDATE ou DELETE.|Abrir para leitura.|A operação de abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|Ambas realizadas com êxito.|  
|Abrir para UPDATE ou DELETE.|Abrir para gravação.|A operação de abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|A operação de abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|  
|Abra para SELECT com leitura repetida.|Abrir para leitura.|Ambas realizadas com êxito.|Ambas realizadas com êxito.|  
|Abra para SELECT com leitura repetida.|Abrir para gravação.|A operação de abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|A operação de abertura da transação 2 falhará com uma exceção ERROR_SHARING_VIOLATION.|  
  
 **Gravação de clientes remotos**  
  
 O acesso do sistema de arquivos remoto a dados FILESTREAM é habilitado pelo protocolo SMB. Se o cliente for remoto, nenhuma operação de gravação será armazenada em cache pelo lado do cliente. Os operações de gravação sempre serão enviados ao servidor. Os dados podem ser armazenados em cache no lado de servidor. Recomendamos que aplicativos que estão em execução em clientes remotos consolidem operações de gravação pequenas para fazer menos operações de gravação usando um tamanho maior de dados.  
  
 Não há suporte para a criação de exibições mapeadas de memória (E/S mapeada de memória) usando um identificador de FILESTREAM. Se o mapeamento de memória for usado para dados FILESTREAM, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não poderá garantir consistência e durabilidade dos dados ou integridade do banco de dados.  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Tarefas relacionadas  
 [Habilitar e configurar FILESTREAM](enable-and-configure-filestream.md)  
  [Criar um banco de dados habilitado para FILESTREAM](create-a-filestream-enabled-database.md)  
  [Criar uma tabela para armazenar dados FILESTREAM](create-a-table-for-storing-filestream-data.md)  
  [Acessar dados FILESTREAM com Transact-SQL](access-filestream-data-with-transact-sql.md)  
  [Criar aplicativos clientes para dados FILESTREAM](create-client-applications-for-filestream-data.md)  
  [Acessar dados do FILESTREAM com OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)  
  [Fazer atualizações parciais em dados do FILESTREAM](make-partial-updates-to-filestream-data.md)  
  [Evitar conflitos com operações de banco de dados em aplicativos FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  [Mover um banco de dados habilitado para FILESTREAM](move-a-filestream-enabled-database.md)  
  [Configurar FILESTREAM em um cluster de failover](set-up-filestream-on-a-failover-cluster.md)  
  [Configurar um firewall para acesso ao FILESTREAM](configure-a-firewall-for-filestream-access.md)  
  
##  <a name="related-content"></a><a name="relcontent"></a> Conteúdo relacionado  
 [Compatibilidade de FILESTREAM com outros recursos de SQL Server](filestream-compatibility-with-other-sql-server-features.md)  
  
