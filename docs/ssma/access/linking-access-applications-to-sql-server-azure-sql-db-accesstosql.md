---
title: Vincular os aplicativos de acesso ao SQL Server - banco de dados SQL do Azure | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/17/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases, linking to SQL Azure
- Access databases, linking to SQL Server
- auto-increment columns
- data types, unsupported
- hyperlink columns
- linking tables
- migrating databases, post-migration issues
- post-migration issues
- reference, post-migration issues
- refreshing linked tables
- slow performance
- unlinking tables
ms.assetid: 82374ad2-7737-4164-a489-13261ba393d4
caps.latest.revision: 19
author: sabotta
ms.author: carlasab
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: 7d5bc198ae3082c1b79a3a64637662968b0748b2
ms.openlocfilehash: 0a0acdf34e916fc3748b0ba33947259e1a361230
ms.contentlocale: pt-br
ms.lasthandoff: 08/17/2017

---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Vinculando a aplicativos de acesso ao SQL Server - banco de dados do SQL do Azure (AccessToSQL)
Se você deseja usar seus aplicativos existentes do Access com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode vincular suas tabelas originais do Access para o migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas do SQL Azure. Vinculação modifica seu banco de dados do Access para que suas páginas de acesso de consultas, formulários, relatórios e dados de usam os dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure em vez dos dados em seu banco de dados do Access.  
  
> [!NOTE]  
> As tabelas de acesso permanecem no Access, mas não são atualizadas em conjunto com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou atualizações do SQL Azure. Depois de vincular as tabelas e verificar a funcionalidade, você talvez queira excluir as tabelas de acesso.  
  
## <a name="linking-access-and-sql-server-tables"></a>Vinculando tabelas de acesso e o SQL Server  
Quando você vincula uma tabela do Access para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabela do SQL Azure, o mecanismo de banco de dados Jet armazena informações de conexão e os metadados da tabela, mas os dados são armazenados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Esse vínculo permite que seus aplicativos do Access operam nas tabelas de acesso, embora a tabelas reais e os dados estão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
> [!NOTE]  
> Se você usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, a senha é armazenada em texto não criptografado em tabelas vinculadas do Access. É recomendável usar a autenticação do Windows.  
  
**Para vincular tabelas**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja vincular.  
  
2.  Clique com botão direito **tabelas**e, em seguida, selecione **Link**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSMA (Migration Assistant) para acesso faz backup da tabela original do acesso e cria uma tabela vinculada.  
  
Depois de vincular as tabelas, as tabelas em SSMA aparecem com um ícone de link pequeno. No Access, as tabelas aparecem com um ícone de "vinculado", que é um globo com uma seta apontando para ele.  
  
Quando você abrir uma tabela no Access, os dados são recuperados usando um cursor de conjunto de chaves. Como resultado, para tabelas grandes, todos os dados não serão recuperados ao mesmo tempo. No entanto, quando você navega pela tabela, o acesso recupera dados adicionais conforme necessário.  
  
> [!IMPORTANT]  
> Para vincular tabelas do access com um banco de dados do Azure, é necessário Client(SNAC) nativo do SQL Server versão 10.5 ou posterior.   
> Você pode obter a versão mais recente do SNAC de [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Desvinculando acessar tabelas  
Quando você desvincula uma tabela de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou restaurações de tabela do SQL Azure, o SSMA a tabela original do Access e seus dados.  
  
**Para desvincular tabelas**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que deseja desvincular.  
  
2.  Clique com botão direito **tabelas**e, em seguida, selecione **desvincular**.  
  
## <a name="linking-tables-to-a-different-server"></a>Vincular tabelas em um servidor diferente  
Se você tiver vinculado as tabelas de acesso a uma instância do SQL Server e depois quiser alterar os links para outra instância, você deve vincular novamente as tabelas.  
  
**Para vincular tabelas em um servidor diferente**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que deseja desvincular.  
  
2.  Clique com botão direito **tabelas** e, em seguida, selecione **desvincular**.  
  
3.  Clique o **reconectar-se ao SQL Server** botão.  
  
4.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure ao qual você deseja vincular as tabelas do Access.  
  
5.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja vincular.  
  
6.  Clique com botão direito **tabelas**e, em seguida, selecione **Link**.  
  
## <a name="updating-linked-tables"></a>Atualizar tabelas vinculadas  
Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou definições de tabela do SQL Azure são alteradas, você poderá desvincular e, em seguida, vincular novamente as tabelas no SSMA usando os procedimentos mostrados anteriormente neste tópico. Você também pode atualizar as tabelas usando o acesso.  
  
**Para atualizar as tabelas vinculadas por meio de acesso**  
  
1.  Abra o banco de dados.  
  
2.  No **objetos** lista, clique em **tabelas**.  
  
3.  Uma tabela vinculada e, em seguida, selecione **Gerenciador de tabelas vinculadas**.  
  
4.  Marque a caixa de seleção ao lado de cada tabela vinculada que você deseja atualizar e, em seguida, clique em **Okey**.  
  
## <a name="possible-post-migration-issues"></a>Possíveis problemas após a migração  
As seções a seguir os problemas de lista que podem ocorrer em aplicativos do Access existentes depois de migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure e, em seguida, vincular as tabelas, junto com as causas e as resoluções.  
  
### <a name="slow-performance-with-linked-tables"></a>Baixo desempenho com tabelas vinculadas  
**Causa:** algumas consultas podem ser lento após upsizing pelos seguintes motivos:  
  
-   O aplicativo depende de funções que não existem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, que faz com que o Jet baixar os tabelas localmente para executar uma consulta SELECT.  
  
-   Consultas que atualizam ou excluem muitas linhas são enviadas pelo Jet como uma consulta parametrizada para cada linha.  
  
**Resolução:** converter as consultas de execução lenta em exibições, procedimentos armazenados ou consultas de passagem. Convertendo em consultas passagem tem os seguintes problemas:  
  
-   Consultas de passagem não podem ser modificadas. Modificando o resultado da consulta ou adição de novos registros deve ser feito em um modo alternativo, como tendo explícita **modificar** ou **adicionar** botões do formulário que está associado à consulta.  
  
-   Algumas consultas exigirem entrada do usuário, mas as consultas de passagem não oferecem suporte a entrada do usuário. Entrada do usuário pode ser obtida pelo Visual Basic para código Applications (VBA) que solicita parâmetros, ou um formulário que é usado como um controle de entrada. Em ambos os casos, o código do VBA envia a consulta com a entrada do usuário para o servidor.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Colunas de incremento automático não são atualizadas até que o registro é atualizado  
**Causa:** depois de chamar RecordSet.AddNew no Jet, a coluna de incremento automático está disponível antes de atualizar o registro. Isso não é verdade em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. O novo valor do valor novo da coluna de identidade está disponível apenas após salvar o novo registro.  
  
**Resolução:** executar o seguinte código Visual Basic for Applications (VBA) antes de acessar o campo de identidade:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>Novos registros não estão disponíveis  
**Causa:** quando você adiciona um registro de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabela do SQL Azure usando o VBA, se o campo de índice exclusivo da tabela tem um valor padrão e você não atribuir um valor para esse campo, o novo registro não aparecerá até que você reabrir a tabela em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Se você tentar obter um valor do registro de novo, a seguinte mensagem de erro será exibida:  
  
`Run-time error '3167' Record is deleted.`  
  
**Resolução:** quando você abre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure de tabela usando o código do VBA, inclua o `dbSeeChanges` opção, como no exemplo a seguir:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Após a migração, algumas consultas não permitirá que o usuário adicione um novo registro  
**Causa:** se uma consulta não inclui todas as colunas que estão incluídas em um índice exclusivo, não é possível adicionar novos valores usando a consulta.  
  
**Resolução:** Certifique-se de que todas as colunas incluídas em pelo menos um índice exclusivo fazem parte da consulta.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>Não é possível modificar um esquema de tabela vinculada com acesso  
**Causa:** após a migração de dados e tabelas de vinculação, o usuário não é possível modificar o esquema de uma tabela do Access.  
  
**Resolução:** modificar o esquema de tabela usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]e, em seguida, atualizar o link no Access.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>Funcionalidade de hiperlink é perdida após migrar dados  
**Causa:** depois de migrar dados, hiperlinks nas colunas perder sua funcionalidade e se tornam mais simples **nvarchar (max)** colunas.  
  
**Resolução:** None.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Não há suporte para alguns tipos de dados do SQL Server pelo Access  
**Causa:** se posteriormente você atualizar seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas SQL Azure contêm tipos de dados que não são suportados pelo Access, você não pode abrir a tabela no Access.  
  
**Resolução:** você pode definir uma consulta de acesso que retorna somente as linhas com tipos de dados com suporte.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

