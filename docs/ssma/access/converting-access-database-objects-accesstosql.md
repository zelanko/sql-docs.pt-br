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
manager: craigg
ms.openlocfilehash: 8137ed37cdbe3bec62e8f7e5a900ade9513894fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735177"
---
# <a name="converting-access-database-objects-accesstosql"></a>Convertendo objetos de banco de dados do Access (AccessToSQL)
Depois de ter adicionado bancos de dados do Access e conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, o SSMA exibe metadados para o acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados do SQL Azure. Você pode agora selecionar objetos de banco de dados do Access e, em seguida, converter os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou esquemas do SQL Azure.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto a partir dos metadados de acesso, converte-os em equivalente [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe e, em seguida, carrega essas informações para o projeto. Você pode exibir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure e suas propriedades usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure.  
  
> [!IMPORTANT]  
> Convertendo objetos não cria os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Ele só converte as definições de objeto e armazena as informações no projeto do SSMA.  
  
Durante a conversão, o SSMA imprime o status para o painel de saída e erro, aviso e mensagens informativas ao painel de lista de erros. Use essas informações para determinar se é necessário modificar seus bancos de dados do Access ou o processo de conversão para obter os resultados da conversão desejada. Você também pode usar as informações de [Preparando bancos de dados de acesso para a migração](preparing-access-databases-for-migration-accesstosql.md) tópico para determinar o que será ou não será convertido.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto na **configurações do projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte colunas de memorando indexada, chaves primárias, restrições de chave estrangeira, os carimbos de hora e tabelas sem índices. Para obter mais informações, consulte [configurações do projeto (conversão)](http://msdn.microsoft.com/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos de acesso são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do SQL Azure:  
  
|Objeto de acesso|Objeto resultante do SQL Server|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|índice|índice|  
|chave estrangeira|chave estrangeira|  
|Consulta|exibição<br /><br />Consultas mais SELECT são convertidas em modos de exibição. Outras consultas, como consultas de atualização não são migradas.<br /><br />Consultas SELECT que usam parâmetros não são convertidas, nem são consultas de referência cruzada.|  
|relatório|não convertido|  
|Formulário|não convertido|  
|macro|não convertido|  
|módulo|não convertido|  
|Valor padrão|Valor padrão|  
|permitir que a propriedade de coluna zero comprimento|restrição de verificação|  
|regra de validação de coluna|restrição de verificação|  
|regra de validação de tabela|restrição de verificação|  
|chave primária|chave primária|  
  
## <a name="converting-access-objects"></a>Converter objetos de acesso  
Para converter objetos de banco de dados do Access, você primeiro deve selecionar os objetos que você deseja converter e, em seguida, ter o SSMA fazer a conversão. Para exibir mensagens de saída durante a conversão na **modo de exibição** menu, selecione **saída**.  
  
**Para selecionar e converter objetos de banco de dados de acesso à sintaxe do SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados de acesso, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
2.  Siga um ou mais destes procedimentos:  
  
    -   Para converter todos os bancos de dados, selecione a caixa de seleção ao lado **bancos de dados**.  
  
    -   Para converter ou omitir os bancos de dados individuais, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir consultas, expanda o banco de dados e, em seguida, marque ou desmarque a **consultas** caixa de seleção.  
  
    -   Para converter ou omitir tabelas individuais, expanda o banco de dados, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Siga um destes procedimentos:  
  
    -   Para converter esquemas, clique com botão direito **bancos de dados** e selecione **converter esquema**.  
  
        Você também pode converter objetos individuais. Para converter um objeto, independentemente de qual objetos selecionados, o objeto com o botão direito e selecione **converter esquema**.  
  
        Quando um objeto tiver sido convertido, ele aparece em negrito no Gerenciador de metadados de acesso.  
  
    -   Para converter, carregar e migrar esquemas e dados em uma única etapa, clique com botão direito bancos de dados e selecione **converter, carregar e migrar**.  
  
4.  Examine as mensagens na **saída** painel e quaisquer erros e avisos na **lista de erros** painel.  
  
## <a name="altering-tables-and-indexes"></a>Alterando tabelas e índices  
Depois de converter metadados de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou metadados do SQL Azure, e antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do SQL Azure, você pode alterar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou índices e tabelas do SQL Azure.  
  
**Para alterar as propriedades de tabela ou índice**  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Gerenciador de metadados do SQL Azure, selecione a tabela ou índice que você deseja alterar.  
  
2.  Sobre o **tabela** guia, clique na propriedade que você deseja alterar e, em seguida, insira ou selecione a nova configuração. Por exemplo, você pode alterar nvarchar(15) para nvarchar (20), ou selecione uma caixa de seleção para tornar uma coluna de tabela que permite valor nulo.  
  
    Mova o cursor para fora na célula da propriedade alterada. Você pode fazer isso clicando em outra linha ou pressionando a tecla Tab.  
  
3.  Clique em **Aplicar**.  
  
Agora você pode exibir as alterações no código na **SQL** guia.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertidos no SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
