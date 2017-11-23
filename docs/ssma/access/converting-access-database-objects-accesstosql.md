---
title: Converter objetos de banco de dados do Access (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9b2240361d87aed6817f2bd5e1b0398ea7fc7894
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="converting-access-database-objects-accesstosql"></a>Converter objetos de banco de dados do Access (AccessToSQL)
Depois de ter adicionado bancos de dados do Access e conectado à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, o SSMA exibe metadados para o acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure. Você pode agora selecionar objetos de banco de dados do Access e, em seguida, converter os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas do SQL Azure.  
  
## <a name="the-conversion-process"></a>O processo de conversão  
Converter objetos de banco de dados usa as definições de objeto a partir dos metadados de acesso, converte-os em equivalente [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxe e, em seguida, carrega essas informações no projeto. Você pode exibir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure e suas propriedades usando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure.  
  
> [!IMPORTANT]  
> Converter objetos não cria os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Ele só converte as definições de objeto e armazena as informações no projeto SSMA.  
  
Durante a conversão, o SSMA imprime o status para o painel de saída e erro, aviso e mensagens informativas para o painel de lista de erros. Use essas informações para determinar se você precisa modificar seus bancos de dados do Access ou o processo de conversão para obter os resultados da conversão desejada. Você também pode usar as informações de [Preparar bancos de dados para migração](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114) tópico para determinar o que será ou não será convertido.  
  
## <a name="setting-conversion-options"></a>Definindo opções de conversão  
Antes de converter objetos, examine as opções de conversão de projeto no **configurações de projeto** caixa de diálogo. Usando essa caixa de diálogo, você pode definir como o SSMA converte colunas de memorando indexada, chaves primárias, restrições de chave estrangeira, os carimbos de hora e tabelas sem índices. Para obter mais informações, consulte [configurações de projeto (conversão)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388)  
  
## <a name="conversion-results"></a>Resultados de conversão  
A tabela a seguir mostra quais objetos de acesso são convertidos e resultante [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos do SQL Azure:  
  
|Objeto de acesso|Objeto resultante do SQL Server|  
|-----------------|-------------------------------|  
|table|table|  
|column|column|  
|índice|índice|  
|chave estrangeira|chave estrangeira|  
|Consulta|exibição<br /><br />Consultas mais SELECT são convertidas em modos de exibição. Outras consultas, como consultas de atualização, não são migradas.<br /><br />SELECIONADAS consultas que usam parâmetros não são convertidas, nem são consultas de tabela de referência cruzada.|  
|relatório|não convertido|  
|formulário|não convertido|  
|macro|não convertido|  
|Módulo|não convertido|  
|Valor padrão|Valor padrão|  
|Permitir zero propriedade da coluna de comprimento|restrição de verificação|  
|regra de validação de coluna|restrição de verificação|  
|regra de validação de tabela|restrição de verificação|  
|chave primária|chave primária|  
  
## <a name="converting-access-objects"></a>Converter objetos de acesso  
Para converter objetos de banco de dados do Access, você deve primeiro selecionar os objetos que você deseja converter e, em seguida, ter SSMA fazer a conversão. Para exibir mensagens de saída durante a conversão no **exibição** menu, selecione **saída**.  
  
**Para selecionar e converter objetos de banco de dados do Access a sintaxe de SQL Server ou SQL Azure**  
  
1.  No Gerenciador de metadados de acesso, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
2.  Siga um ou mais destes procedimentos:  
  
    -   Para converter todos os bancos de dados, selecione a caixa de seleção ao lado de **bancos de dados**.  
  
    -   Para converter ou omitir os bancos de dados individuais, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir consultas, expanda o banco de dados e, em seguida, marque ou desmarque o **consultas** caixa de seleção.  
  
    -   Para converter ou omitir tabelas individuais, expanda o banco de dados, **tabelas**e, em seguida, marque ou desmarque a caixa de seleção ao lado da tabela.  
  
3.  Siga um destes procedimentos:  
  
    -   Para converter esquemas, clique com botão direito **bancos de dados** e selecione **converter esquema**.  
  
        Você também pode converter os objetos individuais. Para converter um objeto, independentemente de quais objetos são selecionados, clique no objeto e selecione **converter esquema**.  
  
        Quando um objeto tiver sido convertido, ele aparece em negrito no Gerenciador de metadados de acesso.  
  
    -   Para converter, carregar e migrar esquemas e dados em uma única etapa, clique em bancos de dados e selecione **converter, carregar e migrar**.  
  
4.  Examine as mensagens no **saída** painel e os erros e avisos no **lista de erros** painel.  
  
## <a name="altering-tables-and-indexes"></a>Alterando tabelas e índices  
Depois de converter metadados de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou metadados do SQL Azure, e antes de carregar os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você pode alterar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou índices e tabelas do SQL Azure.  
  
**Para alterar as propriedades da tabela ou índice**  
  
1.  Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados do SQL Azure, selecione a tabela ou índice que você deseja alterar.  
  
2.  Sobre o **tabela** guia, clique na propriedade que você deseja alterar e, em seguida, insira ou selecione a nova configuração. Por exemplo, você pode alterar nvarchar (15) para nvarchar (20) ou marque uma caixa de seleção para tornar a coluna de tabela permite valor nulo.  
  
    Mova o cursor para fora da célula da propriedade alterada. Você pode fazer isso clicando em outra linha ou pressionando a tecla Tab.  
  
3.  Clique em **Aplicar**.  
  
Agora você pode exibir as alterações no código no **SQL** guia.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [carregar objetos de banco de dados convertido no SQL Server](http://msdn.microsoft.com/en-us/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba)  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
