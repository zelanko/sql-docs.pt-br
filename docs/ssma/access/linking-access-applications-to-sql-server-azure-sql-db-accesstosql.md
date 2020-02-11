---
title: Vincular aplicativos de acesso a SQL Server-banco de BD SQL do Azure | Microsoft Docs
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
ms.openlocfilehash: c4e6d16645b8a7ecab9ed2e814ed345834e80f1b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245924"
---
# <a name="linking-access-applications-to-sql-server---azure-sql-db-accesstosql"></a>Vinculando aplicativos de acesso ao SQL Server – BD SQL do Azure (AccessToSQL)
Se você quiser usar seus aplicativos do Access existentes com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, poderá vincular suas tabelas originais do Access às tabelas migradas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. A vinculação modifica o banco de dados do Access de forma que suas consultas, formulários, relatórios e páginas de acesso a data [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usem os dados do banco de dados do ou do SQL Azure em vez de usarem o banco de dado do Access.  
  
> [!NOTE]  
> Suas tabelas do Access permanecem no acesso, mas não são atualizadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] junto com ou SQL Azure atualizações. Depois de vincular as tabelas e verificar a funcionalidade, talvez você queira excluir suas tabelas do Access.  
  
## <a name="linking-access-and-sql-server-tables"></a>Vinculando acesso e tabelas de SQL Server  
Quando você vincula uma tabela de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma tabela do ou SQL Azure, o mecanismo de banco de dados Jet armazena informações de conexão e metadados de tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas os dados são armazenados no ou SQL Azure. Essa vinculação permite que seus aplicativos de acesso operem nas tabelas do Access, mesmo que as tabelas e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os dados reais estejam no ou SQL Azure.  
  
> [!NOTE]  
> Se você usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a autenticação do, sua senha será armazenada em texto não criptografado nas tabelas de acesso vinculadas. É recomendável usar a autenticação do Windows.  
  
**Para vincular tabelas**  
  
1.  No Gerenciador de metadados do Access, selecione as tabelas que você deseja vincular.  
  
2.  Clique com o botão direito do mouse em **tabelas**e selecione **vincular**.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Assistente de Migração (SSMA) para Access faz backup da tabela de acesso original e cria uma tabela vinculada.  
  
Depois de vincular as tabelas, as tabelas no SSMA aparecem com um ícone de link pequeno. No Access, as tabelas aparecem com um ícone "vinculado", que é um globo com uma seta apontando para ela.  
  
Quando você abre uma tabela no Access, os dados são recuperados usando um cursor do conjunto de chaves. Como resultado, para tabelas grandes, todos os dados não são recuperados ao mesmo tempo. No entanto, à medida que você navega pela tabela, o Access recupera dados adicionais conforme necessário.  
  
> [!IMPORTANT]  
> Para vincular tabelas de acesso a um banco de dados do Azure, você precisa do SQL Server Native Client (SNAC) versão 10,5 ou superior.   
> Você pode obter a versão mais recente do SNAC do [Microsoft® SQL Server® 2008 R2 Feature Pack](https://www.microsoft.com/download/details.aspx?id=16978).  
  
## <a name="unlinking-access-tables"></a>Desvinculando tabelas de acesso  
Quando você desvincula uma tabela de acesso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma tabela do ou SQL Azure, o SSMA restaura a tabela de acesso original e seus dados.  
  
**Para desvincular tabelas**  
  
1.  No Gerenciador de metadados do Access, selecione as tabelas que você deseja desvincular.  
  
2.  Clique com o botão direito do mouse em **tabelas**e selecione **desvincular**.  
  
## <a name="linking-tables-to-a-different-server"></a>Vinculando tabelas a um servidor diferente  
Se você tiver vinculado as tabelas do Access a uma instância do SQL Server e posteriormente desejar alterar os links para outra instância, será necessário vincular novamente as tabelas.  
  
**Para vincular tabelas a um servidor diferente**  
  
1.  No Gerenciador de metadados do Access, selecione as tabelas que você deseja desvincular.  
  
2.  Clique com o botão direito do mouse em **tabelas** e selecione **desvincular**.  
  
3.  Clique no botão **reconectar-se a SQL Server** .  
  
4.  Conecte-se à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do ou SQL Azure ao qual você deseja vincular as tabelas do Access.  
  
5.  No Gerenciador de metadados do Access, selecione as tabelas que você deseja vincular.  
  
6.  Clique com o botão direito do mouse em **tabelas**e selecione **vincular**.  
  
## <a name="updating-linked-tables"></a>Atualizando tabelas vinculadas  
Se as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de tabela do ou SQL Azure forem alteradas, você poderá desvincular e, em seguida, vincular novamente as tabelas no SSMA usando os procedimentos mostrados anteriormente neste tópico. Você também pode atualizar as tabelas usando o Access.  
  
**Para atualizar tabelas vinculadas usando o Access**  
  
1.  Abra o banco de dados do Access.  
  
2.  Na lista **objetos** , clique em **tabelas**.  
  
3.  Clique com o botão direito do mouse em uma tabela vinculada e selecione **Gerenciador de tabela vinculada**.  
  
4.  Marque a caixa de seleção ao lado de cada tabela vinculada que você deseja atualizar e clique em **OK**.  
  
## <a name="possible-post-migration-issues"></a>Possíveis problemas após a migração  
As seções a seguir listam os problemas que podem ocorrer em aplicativos do Access existentes depois que você migrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados de acesso para ou SQL Azure e, em seguida, vincular as tabelas, junto com as causas e as resoluções.  
  
### <a name="slow-performance-with-linked-tables"></a>Desempenho lento com tabelas vinculadas  
**Causa:** Algumas consultas podem ser lentas após o upsizing pelos seguintes motivos:  
  
-   O aplicativo depende de funções que não existem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, o que faz com que o Jet receba tabelas localmente para executar uma consulta SELECT.  
  
-   As consultas que atualizam ou excluem muitas linhas são enviadas pelo Jet como uma consulta parametrizada para cada linha.  
  
**Resolução:** Converta as consultas de execução lenta em consultas de passagem, procedimentos armazenados ou exibições. A conversão para consultas de passagem tem os seguintes problemas:  
  
-   As consultas de passagem não podem ser modificadas. A modificação do resultado da consulta ou a adição de novos registros deve ser feita de forma alternativa, por exemplo, com a **modificação** **explícita ou a adição de** botões no formulário associado à consulta.  
  
-   Algumas consultas exigem entrada do usuário, mas as consultas de passagem não dão suporte à entrada do usuário. A entrada do usuário pode ser obtida pelo código Visual Basic for Applications (VBA) que solicita parâmetros ou por um formulário que é usado como um controle de entrada. Em ambos os casos, o código VBA envia a consulta com a entrada do usuário para o servidor.  
  
### <a name="auto-increment-columns-are-not-updated-until-the-record-is-updated"></a>Colunas de incremento automático não são atualizadas até que o registro seja atualizado  
**Causa:** Depois de chamar RecordSet. AddNew no Jet, a coluna de incremento automático estará disponível antes da atualização do registro. Isso não é verdadeiro no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. O novo valor da coluna de identidade novo valor está disponível somente depois de salvar o novo registro.  
  
**Resolução:** Execute o seguinte código de Visual Basic for Applications (VBA) antes de acessar o campo de identidade:  
  
```  
Recordset.Update  
Recordset.Move 0,  
Recordset.LastModified  
```  
  
### <a name="new-records-are-not-available"></a>Novos registros não estão disponíveis  
**Causa:** Quando você adiciona um registro a uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela do ou SQL Azure usando o VBA, se o campo índice exclusivo da tabela tiver um valor padrão e você não atribuir um valor a esse campo, o novo registro não aparecerá até que você reabra a tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou SQL Azure. Se você tentar obter um valor do novo registro, receberá a seguinte mensagem de erro:  
  
`Run-time error '3167' Record is deleted.`  
  
**Resolução:** Quando você abre a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela ou SQL Azure usando o código do VBA, inclua `dbSeeChanges` a opção, como no exemplo a seguir:  
  
`Set rs = db.OpenRecordset("TestTable", dbOpenDynaset, dbSeeChanges)`  
  
### <a name="after-migration-some-queries-will-not-allow-the-user-to-add-a-new-record"></a>Após a migração, algumas consultas não permitirão que o usuário adicione um novo registro  
**Causa:** Se uma consulta não incluir todas as colunas incluídas em um índice exclusivo, você não poderá adicionar novos valores usando a consulta.  
  
**Resolução:** Verifique se todas as colunas incluídas em pelo menos um índice exclusivo fazem parte da consulta.  
  
### <a name="you-cannot-modify-a-linked-table-schema-with-access"></a>Não é possível modificar um esquema de tabela vinculada com acesso  
**Causa:** Depois de migrar dados e vincular tabelas, o usuário não pode modificar o esquema de uma tabela no Access.  
  
**Resolução:** Modifique o esquema de tabela usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e, em seguida, atualize o link no Access.  
  
### <a name="hyperlink-functionality-is-lost-after-migrating-data"></a>A funcionalidade de hiperlink é perdida após a migração de dados  
**Causa:** Após a migração de dados, os hiperlinks em colunas perdem sua funcionalidade e se tornam colunas **nvarchar (max)** simples.  
  
**Resolução:** None.  
  
### <a name="some-sql-server-data-types-are-not-supported-by-access"></a>Não há suporte para alguns tipos de dados SQL Server pelo Access  
**Causa:** Se você atualizar mais tarde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suas tabelas ou SQL Azure para conter tipos de dados que não têm suporte do Access, não será possível abrir a tabela no Access.  
  
**Resolução:** Você pode definir uma consulta de acesso que retorna somente as linhas com tipos de dados com suporte.  
  
## <a name="see-also"></a>Confira também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
