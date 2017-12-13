---
title: Compatibilidade de FileTable com outros recursos do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: blob
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
caps.latest.revision: "19"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f1d34f1aef0eddb13a57860fa8eb9f4219ec577
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>Compatibilidade do FileTable com outros recursos do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Descreve como as FileTables funcionam com outros recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="alwayson"></a> Grupos de disponibilidade AlwaysOn e FileTables  
 Quando o banco de dados que contém dados FILESTREAM ou FileTable pertence a um grupo de disponibilidade AlwaysOn:  
  
-   A funcionalidade FileTable tem suporte parcial pelo [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Depois de um failover, os dados de FileTable estarão acessíveis na réplica primária, mas os dados de FileTable não estarão acessíveis em réplicas secundárias legíveis.  
  
    > **OBSERVAÇÃO:**  observe que, após um failover, haverá suporte toda a funcionalidade de FILESTREAM. Os dados de FILESTREAM podem ser acessados em ambas as réplicas secundárias legíveis e no novo primário.  
  
-   As funções FILESTREAM e FileTable aceitam ou retornam VNNs (nomes de rede virtual) em vez de nomes de computadores. Para obter mais informações sobre essas funções, veja [Funções Filestream e FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Todo o acesso aos dados FILESTREAM ou FileTable pelas APIs do sistema de arquivos deve usar VNNs em vez de nomes de computadores. Para obter mais informações, consulte [FILESTREAM e FileTable com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
##  <a name="OtherPartitioning"></a> Particionamento e FileTables  
 Não há suporte para particionamento em FileTables. Com o suporte para vários grupos de arquivos FILESTREAM, problemas simples de expansão podem ser resolvidos sem o uso do recurso de particionamento na maioria dos cenários (ao contrário de FILESTREAMs do SQL 2008).  
  
##  <a name="OtherRepl"></a> Replicação e FileTables  
 Não há suporte para replicação e recursos relacionados (inclusive replicação transacional, replicação de mesclagem, change data capture e controle de alterações) com FileTables.  
  
##  <a name="OtherIsolation"></a> Semântica de transação e FileTables  
 **Aplicativos do Windows**  
 Os aplicativos do Windows não entendem transações de banco de dados; então as operações de gravação do Windows não fornecem as propriedades ACID de uma transação de banco de dados. Portanto, as reversões e a recuperação transacionais não são possíveis com operações de atualização do Windows.  
  
 **Aplicativos Transact-SQL**  
 Para os aplicativos TSQL que funcionam na coluna FILESTREAM (file_stream) em uma FileTable, as semânticas de isolamento são iguais às do tipo de dados FILESTREAM em uma tabela de usuário normal.  
  
##  <a name="OtherQueryNot"></a> Notificações de consulta e FileTables  
 A consulta não pode conter referência à coluna FILESTREAM na FileTable, na cláusula WHERE ou em qualquer outra parte da consulta.  
  
##  <a name="OtherSelectInto"></a> SELECT INTO e FileTables  
 As instruções SELECT INTO de uma FileTable não propagarão a semântica da FileTable na tabela de destino criada (da mesma forma que as colunas FILESTREAM em uma tabela normal). Todas as colunas da tabela de destino se comportarão como colunas normais. Elas não terão nenhuma semântica de FileTable associada.  
  
##  <a name="OtherTriggers"></a> Gatilhos e FileTables  
 **Gatilhos DDL (linguagem de definição de dados)**  
 Não há nenhuma consideração especial para gatilhos DDL com FileTables. Gatilhos DDL normais acionarão as operações Create/Alter database, além das operações CREATE/ALTER TABLE para FileTables. Os gatilhos podem recuperar os dados de eventos reais, que incluem o texto do comando DDL e outras informações por meio da chamada da função EVENTDATA(). Não há nenhum novo evento ou alteração do esquema Eventdata existente.  
  
 **Gatilhos DML (linguagem de manipulação de dados)**  
 Estas restrições serão impostas durante a operação DDL para criar gatilhos.  
  
-   As FileTables NÃO oferecem suporte a gatilhos INSTEAD OF para operações DML. Essa é uma restrição existente em todas as tabelas que contêm colunas FILESTREAM.  
  
-   As FileTables oferecerão suporte a gatilhos AFTER para operações DML.  
  
-   Os gatilhos definidos em uma FileTable não podem atualizar FileTables (inclusive a FileTable pai). Essa restrição existe principalmente para impedir que um gatilho entre em conflitos de bloqueio com bloqueios mantidos pelo acesso ao sistema de arquivos na mesma transação.  
  
 **Acesso não transacional e seus efeitos em gatilhos**  
 -   Quando o acesso de atualização não transacional é permitido em um banco de dados, é possível fazer uma atualização in loco dos dados FILESTREAM em qualquer tabela, inclusive FileTable, nesse banco de dados. Devido a essa possibilidade, a imagem anterior do conteúdo FILESTREAM talvez não esteja disponível para ser usada pelo gatilho.  
  
-   Para operações de atualização não transacionais através do sistema de arquivos, o SQL Server criará uma transação interna para capturar a operação CloseHandle, e qualquer gatilho DML definido poderá ser disparado como parte dessa transação. Uma reversão, como uma transação dentro do corpo do gatilho, embora não esteja impedida, não reverte as alterações feitas no FILESTREAM.  Tal reversão também pode impedir o disparo de gatilhos Update, mesmo que o conteúdo FILESTREAM possa ter sido alterado.  
  
-   Além desses impactos, os gatilhos em FileTables precisam lidar com alguns comportamentos adicionais  
  
    -   No caso de operações de atualização não transacionais em uma FileTable através do sistema de arquivos, é possível que o conteúdo FILESTREAM seja bloqueado exclusivamente por outras operações Win32 e não estejam acessíveis para leitura/gravação por meio do corpo do gatilho. Nesses casos, qualquer tentativa de acessar o conteúdo FILESTREAM dentro do corpo do gatilho pode resultar em um erro de "Violação de Compartilhamento". Os gatilhos devem ser criados para tratar esses erros de maneira adequada.  
  
    -   A imagem AFTER do FILESTREAM pode não ser estável porque, na maioria dos casos, pode estar sendo ativamente gravada por outras atualizações não transacionais ao mesmo tempo (devido aos modos de compartilhamento permitidos no acesso ao sistema de arquivos).  
  
-   O encerramento anormal de identificadores Win32, como a eliminação explícita de identificadores Win32 por um administrador OU uma pane do banco de dados, não executará gatilhos de usuário durante as operações de recuperação, embora o conteúdo FILESTREAM possa ter sido alterado pelo aplicativo Win32 encerrado de forma anormal.  
  
##  <a name="OtherViews"></a> Exibições e FileTables  
 **Exibições**  
 Uma exibição pode ser criada em um FileTable como em qualquer outra tabela. Entretanto, as considerações a seguir se aplicam a uma exibição criada em uma FileTable:  
  
-   A exibição não terá nenhuma semântica de FileTable. Isso é, as colunas na exibição (inclusive as colunas de Atributos de Arquivo) se comportam da mesma forma que as colunas de exibição normais, sem qualquer semântica especial, e o mesmo acontece para as linhas que representam Arquivos/diretórios.  
  
-   A exibição pode ser atualizada com base na semântica de "exibição atualizável", mas as restrições de tabela subjacentes podem rejeitar as atualizações, como na tabela.  
  
-   Você pode visualizar o caminho de um arquivo na exibição adicionando-o como uma coluna explícita na exibição. Por exemplo:  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, …, GetFileNamespacePath() AS PATH, column3,…  FROM Documents`  
  
 **Exibições indexadas**  
 Atualmente, as exibições indexadas não podem incluir colunas FILESTREAM ou colunas computadas/computadas persistentes que dependem das colunas FILESTREAM. Esse comportamento permanece inalterado com as exibições também definidas na FileTable.  
  
##  <a name="OtherSnapshots"></a> Isolamento de instantâneo e FileTables  
 O RCSI (isolamento de instantâneo de leitura confirmada) e o SI (isolamento de instantâneo) dependem da capacidade de ter um instantâneo dos dados disponível para leitores quando operações de atualização estão ocorrendo nos dados. Entretanto, as FileTables permitem o acesso de gravação não transacional aos dados do fluxo de dados. Como resultado, as restrições a seguir se aplicam ao uso desses recursos em bancos de dados que contêm FileTables:  
  
-   Um banco de dados que contém FileTables pode ser alterado para habilitar o RCSI/SI.  
  
-   Quando o acesso não transacional está definido como FULL para o banco de dados, uma transação sendo executada no RCSI ou SI tem o seguinte comportamento:  
  
    -   Qualquer leitura do [!INCLUDE[tsql](../../includes/tsql-md.md)] da coluna file_stream de FileTable falharia. INSERT e UPDATE para a coluna teriam êxito, contanto que não lessem a partir da coluna file_stream.  
  
    -   Se a instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)] especificar dicas da tabela READCOMMITTEDLOCK, as leituras terão êxito, e aplicarão bloqueios nas linhas, em vez de usar o controle de versão de linha.  
  
    -   As solicitações abertas de FileStream Win32 transacionado também falhariam.  
  
    -   O acesso não transacionado Win32 a FileTable terá êxito. Todas as consultas internas feitas pela FileTable não são afetadas.  
  
    -   A indexação de texto completo sempre terá êxito, não importa quais sejam as opções de banco de dados (READ_COMMITTED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION).  
  
##  <a name="readsec"></a> Bancos de dados secundários legíveis  
 As mesmas considerações se aplicam a bancos de dados secundários legíveis sobre instantâneos, como descrito na seção acima, [Isolamento de instantâneo e FileTables](#OtherSnapshots).  
  
##  <a name="CDB"></a> Bancos de dados independentes e FileTables  
 O recurso FILESTREAM do qual o recurso FileTable depende exige alguma configuração fora do banco de dados. Portanto, um banco de dados que usa FILESTREAM ou FileTable não é contido completamente.  
  
 Você poderá definir a retenção de banco de dados como PARTIAL se desejar usar determinados recursos de bancos de dados contidos, como usuários contidos. Neste caso, no entanto, você deve estar atento que algumas das configurações de banco de dados não estão contidas no banco de dados e não são movidos automaticamente quando o banco de dados é movido.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
