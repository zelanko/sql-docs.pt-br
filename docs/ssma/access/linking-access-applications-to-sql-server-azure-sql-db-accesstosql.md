---
title: Vincular aplicativos do Access para o SQL Server – BD SQL do Azure | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 20efdf681baa8305b3b2be08b2e9f3efe999d3fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760141"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Vincular aplicativos do Access para o SQL Server – BD SQL do Azure (AccessToSQL)
Se você deseja usar seus aplicativos existentes do Access com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode vincular suas tabelas originais do Access para o migrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabelas do SQL Azure. Vinculação modifica seu banco de dados do Access, para que suas páginas de acesso de consultas, formulários, relatórios e dados de usarem os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados do SQL Azure em vez dos dados em seu banco de dados do Access.  
  
> [!NOTE]  
> Suas tabelas do Access permanecem no Access, mas não são atualizadas em conjunto com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou atualizações do SQL Azure. Depois de vincular as tabelas e verificar a funcionalidade, você talvez queira excluir suas tabelas do Access.  
  
## <a name="linking-access-and-sql-server-tables"></a>Vinculando tabelas de acesso e o SQL Server  
Quando você vincular uma tabela do Access para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a tabela do SQL Azure, o mecanismo de banco de dados Jet armazena informações de conexão e metadados de tabela, mas os dados são armazenados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Essa vinculação permite que seus aplicativos do Access operam nas tabelas de acesso, mesmo que as tabelas reais e os dados estão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure.  
  
> [!NOTE]  
> Se você usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, sua senha é armazenada em texto não criptografado em tabelas vinculadas do Access. É recomendável usar a autenticação do Windows.  
  
**Ao vincular tabelas**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja vincular.  
  
2.  Clique com botão direito **tabelas**e, em seguida, selecione **Link**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para acesso ao backup da tabela de acesso original e cria uma tabela vinculada.  
  
Depois de vincular as tabelas, as tabelas no SSMA aparecem com um ícone de link pequeno. Em acesso, as tabelas aparecem com um ícone de "vinculado", que é um mundo com uma seta apontando para ele.  
  
Quando você abre uma tabela no Access, os dados são recuperados usando um cursor keyset. Como resultado, para tabelas grandes, todos os dados não são recuperados ao mesmo tempo. No entanto, enquanto você navega por meio da tabela, o Access recupera dados adicionais conforme necessário.  
  
> [!IMPORTANT]  
> Para vincular a tabelas do access com um banco de dados do Azure, você precisa Client(SNAC) nativo do SQL Server versão 10.5 ou posterior.   
> Você pode obter a versão mais recente do SNAC partir [Microsoft® SQL Server® 2008 R2 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=196940).  
  
## <a name="unlinking-access-tables"></a>Desvinculando acessar tabelas  
Quando você desvincula uma tabela do Access de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabela do SQL Azure, o SSMA restaura a tabela de acesso original e seus dados.  
  
**Para desvincular tabelas**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja desvincular.  
  
2.  Clique com botão direito **tabelas**e, em seguida, selecione **desvincular**.  
  
## <a name="linking-tables-to-a-different-server"></a>Vinculando tabelas em um servidor diferente  
Se você tiver vinculado as tabelas de acesso a uma instância do SQL Server e depois quiser alterar os links para outra instância, você deve vincular novamente as tabelas.  
  
**Para vincular tabelas em um servidor diferente**  
  
1.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja desvincular.  
  
2.  Clique com botão direito **tabelas** e, em seguida, selecione **desvincular**.  
  
3.  Clique o **reconectar-se ao SQL Server** botão.  
  
4.  Conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure ao qual você deseja vincular as tabelas do Access.  
  
5.  No Gerenciador de metadados de acesso, selecione as tabelas que você deseja vincular.  
  
6.  Clique com botão direito **tabelas**e, em seguida, selecione **Link**.  
  
## <a name="updating-linked-tables"></a>Atualizar tabelas vinculadas  
Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou definições de tabela do SQL Azure são alteradas, você pode desvincular e, em seguida, vincule novamente as tabelas no SSMA usando os procedimentos mostrados anteriormente neste tópico. Você também pode atualizar as tabelas por meio do acesso.  
  
**Para atualizar tabelas vinculadas por meio do acesso**  
  
1.  Abra o banco de dados.  
  
2.  No **objetos** , clique em **tabelas**.  
  
3.  Uma tabela vinculada e, em seguida, selecione **Gerenciador de tabelas vinculadas**.  
  
4.  Marque a caixa de seleção ao lado de cada tabela vinculada que você deseja atualizar e, em seguida, clique em **Okey**.  
  
## <a name="possible-post-migration-issues"></a>Possíveis problemas após a migração  
As seções a seguir os problemas de lista que podem ocorrer em aplicativos do Access existentes após a migração de bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure e, em seguida, vincule as tabelas, juntamente com as causas e resoluções executadas o.  
  
### <a name="slow-performance-with-linked-tables"></a>Lentidão no desempenho com tabelas vinculadas  
**Causa:** Algumas consultas podem ser lentas após as upsizing pelos seguintes motivos:  
  
-   O aplicativo depende de funções que não existem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, que faz com que o Jet puxar tabelas localmente para executar uma consulta SELECT.  
  
-   Consultas que atualizam ou excluem o número de linhas são enviadas pelo Jet como uma consulta parametrizada para cada linha.  
  
**Resolução:** Converta as consultas lentas em exibições, procedimentos armazenados ou consultas de passagem. Convertendo em consultas de passagem tem os seguintes problemas:  
  
-   Consultas de passagem não podem ser modificadas. Modificar o resultado da consulta ou adicionar novos registros deve ser feito em um modo alternativo, como tendo explícito **Modify** ou **adicionar** botões no formulário que está associado à consulta.  
  
-   Algumas consultas exigem a entrada do usuário, mas as consultas de passagem não dão suporte a entrada do usuário. Entrada do usuário pode ser obtida pelo Visual Basic para o código de aplicativos (VBA) que solicita parâmetros, ou por um formulário que é usado como um controle de entrada. Em ambos os casos, o código do VBA envia a consulta com a entrada do usuário para o servidor.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Colunas de incremento automático não são atualizadas até que o registro é atualizado  
**Causa:** Depois de chamar RecordSet.AddNew no Jet, a coluna de incremento automático está disponível antes do registro é atualizado. Isso não é válido em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. O novo valor do valor novo da coluna de identidade está disponível somente depois de salvar o novo registro.  
  
**Resolução:** Execute o seguinte código Visual Basic for Applications (VBA) antes de acessar o campo de identidade:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>Novos registros não estão disponíveis  
**Causa:** Quando você adiciona um registro de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a tabela do SQL Azure usando o VBA, se o campo de índice exclusivo da tabela tem um valor padrão e você não atribuir um valor para esse campo, o novo registro não aparece até que você reabrir a tabela em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Se você tentar obter um valor do novo registro, a seguinte mensagem de erro será exibida:  
  
`Run-time error '3167' Record is deleted.`  
  
**Resolução:** Quando você abre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure de tabela usando o código VBA, inclua o `dbSeeChanges` opção, como no exemplo a seguir:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Após a migração, algumas consultas não permitirá que o usuário adicione um novo registro  
**Causa:** Se uma consulta não inclui todas as colunas que estão incluídas em um índice exclusivo, será possível adicionar novos valores usando a consulta.  
  
**Resolução:** Certifique-se de que todas as colunas incluídas em pelo menos um índice exclusivo são parte da consulta.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>Não é possível modificar um esquema de tabela vinculada com acesso  
**Causa:** Após a migração de dados e tabelas de vinculação, o usuário não é possível modificar o esquema de uma tabela no Access.  
  
**Resolução:** Modificar o esquema da tabela usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, em seguida, atualizar o link no Access.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>Funcionalidade de hiperlink é perdida depois de migrar dados  
**Causa:** Depois de migrar dados, perder sua funcionalidade e se tornam mais simples de hiperlinks nas colunas **nvarchar (max)** colunas.  
  
**Resolução:** Nenhum.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Não há suporte para alguns tipos de dados do SQL Server por acesso  
**Causa:** Se você atualizar posteriormente suas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tabelas do SQL Azure contêm tipos de dados que não são compatíveis com acesso, você não pode abrir a tabela no Access.  
  
**Resolução:** Você pode definir uma consulta que retorna somente as linhas com tipos de dados com suporte do Access.  
  
## <a name="see-also"></a>Confira também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
