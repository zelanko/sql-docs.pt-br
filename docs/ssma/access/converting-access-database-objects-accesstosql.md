---
title: Convertendo objetos de banco de dados do Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, converting schemas
- conversion
- conversion, converting schemas
- indexes, altering
- metadata
- metadata, altering
- metadata, converting
- migrating databases, one-click
- one-click migration
- schemas
- schemas, converting
- SQL
- SQL, converting
- syntax
- syntax, converting
- tables, altering
- translating Access to SQL Azure
- translating Access to SQL Server
ms.assetid: e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 56c55dbc5df61bfdb9013e505335af16fccbeecd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68006623"
---
# <a name="converting-access-database-objects-accesstosql"></a>Convertendo AccessToSQL (objetos de banco de dados do Access)
Depois de adicionar bancos de dados do Access e conectados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, o SSMA exibe os metadados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acesso e ou SQL Azure objetos de banco de dados. Agora você pode selecionar acessar objetos de banco de dados e, em seguida, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converter os esquemas em ou SQL Azure esquemas.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
A conversão de objetos de banco de dados usa as definições de objeto dos metadados de [!INCLUDE[tsql](../../includes/tsql-md.md)] acesso, converte-os em sintaxe equivalente e, em seguida, carrega essas informações no projeto. Em seguida, você pode [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exibir os objetos ou SQL Azure e suas propriedades [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando ou SQL Azure o Gerenciador de metadados.  
  
> [!IMPORTANT]  
> A conversão de objetos não cria os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou SQL Azure. Ele apenas converte as definições de objeto e armazena as informações no projeto do SSMA.  
  
Durante a conversão, o SSMA imprime o status no painel de saída e mensagens de erro, aviso e informativas no painel de Lista de Erros. Use essas informações para determinar se você precisa modificar seus bancos de dados do Access ou seu processo de conversão para obter os resultados de conversão desejados. Você também pode usar as informações no tópico [preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md) para determinar o que será e não será convertido.  
  
## <a name="setting-conversion-options"></a>Configurando opções de conversão  
Antes de converter objetos, examine as opções de conversão do projeto na caixa de diálogo **configurações do projeto** . Usando essa caixa de diálogo, você pode definir como o SSMA Converte colunas de memorando indexadas, chaves primárias, restrições de chave estrangeira, carimbos de data/hora e tabelas sem índices. Para obter mais informações, consulte [configurações do projeto (conversão)](https://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Resultados da conversão  
A tabela a seguir mostra quais objetos de acesso são convertidos e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os objetos resultantes ou SQL Azure:  
  
|Objeto de acesso|Objeto SQL Server resultante|  
|-----------------|-------------------------------|  
|tabela|tabela|  
|coluna|coluna|  
|índice|índice|  
|chave estrangeira|chave estrangeira|  
|Consulta|exibição<br /><br />A maioria das consultas SELECT são convertidas em exibições. Outras consultas, como consultas de atualização, não são migradas.<br /><br />As consultas selecionadas que usam parâmetros não são convertidas nem consultas entre guias.|  
|relatório|Não convertido|  
|formulário|Não convertido|  
|Macro |Não convertido|  
|module|Não convertido|  
|valor padrão|valor padrão|  
|Propriedade de coluna permitir comprimento zero|restrição de verificação|  
|regra de validação de coluna|restrição de verificação|  
|regra de validação de tabela|restrição de verificação|  
|chave primária|chave primária|  
  
## <a name="converting-access-objects"></a>Convertendo objetos do Access  
Para converter objetos de banco de dados do Access, primeiro você deve selecionar os objetos que deseja converter e, em seguida, fazer com que o SSMA faça a conversão. Para exibir mensagens de saída durante a conversão, no menu **Exibir** , selecione **saída**.  
  
**Para selecionar e converter objetos de banco de dados do Access para SQL Server ou sintaxe de SQL Azure**  
  
1.  No Gerenciador de metadados do Access, expanda **acesso-metabase**e expanda **bancos de dados**.  
  
2.  Execute uma ou mais das seguintes opções:  
  
    -   Para converter todos os bancos de dados, marque a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir bancos de dados individuais, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir consultas, expanda o banco de dados e marque ou desmarque a caixa de seleção **consultas** .  
  
    -   Para converter ou omitir tabelas individuais, expanda o banco de dados, expanda **tabelas**e marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Realize um dos seguintes procedimentos:  
  
    -   Para converter esquemas, clique com o botão direito do mouse em **bancos de dados** e selecione **converter esquema**.  
  
        Você também pode converter objetos individuais. Para converter um objeto, independentemente dos objetos selecionados, clique com o botão direito do mouse no objeto e selecione **converter esquema**.  
  
        Quando um objeto tiver sido convertido, ele aparecerá em negrito no Gerenciador de metadados do Access.  
  
    -   Para converter, carregar e migrar esquemas e dados em uma única etapa, clique com o botão direito do mouse em bancos e selecione **converter, carregar e migrar**.  
  
4.  Examine as mensagens no painel de **saída** e quaisquer erros e avisos no painel de **lista de erros** .  
  
## <a name="altering-tables-and-indexes"></a>Alterando tabelas e índices  
Depois de converter os metadados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acesso para ou SQL Azure metadados e antes de carregar os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ou SQL Azure, você pode [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alterar ou SQL Azure tabelas e índices.  
  
**Para alterar as propriedades da tabela ou do índice**  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados, selecione a tabela ou o índice que você deseja alterar.  
  
2.  Na guia **tabela** , clique na propriedade que você deseja alterar e, em seguida, digite ou selecione a nova configuração. Por exemplo, você pode alterar nvarchar (15) para nvarchar (20) ou marcar uma caixa de seleção para tornar a coluna de tabela anulável.  
  
    Mover o cursor para fora da célula de propriedade alterada. Você pode fazer isso clicando em outra linha ou pressionando a tecla Tab.  
  
3.  Clique em **Aplicar**.  
  
Agora você pode exibir as alterações no código na guia **SQL** .  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos em SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
