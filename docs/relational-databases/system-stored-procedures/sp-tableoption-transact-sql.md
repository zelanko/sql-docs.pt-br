---
description: sp_tableoption (Transact-SQL)
title: sp_tableoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 06655c8dd684ca89d6e67b065d3943ee57f752fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473555"
---
# <a name="sp_tableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Define valores de opção para tabelas definidas pelo usuário. sp_tableoption pode ser usado para controlar o comportamento na linha de tabelas com **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **XML**, **Text**, **ntext**, **Image**ou colunas de tipo definido pelo usuário grande.  
  
> [!IMPORTANT]  
>  O recurso text in row será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para armazenar dados de valor grande, recomendamos que você use os tipos de dados **varchar (max)**, **nvarchar (max)** e **varbinary (max)** .  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @TableNamePattern =] '*tabela*'  
 É o nome qualificado ou não qualificado de uma tabela de banco de dados definida pelo usuário. Se um nome de tabela totalmente qualificado, incluindo um nome de banco de dados, for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual. Não se pode definir opções de tabela para várias tabelas ao mesmo tempo. *Table* é **nvarchar (776)**, sem padrão.  
  
 [ @OptionName =] '*option_name*'  
 É um nome de opção de tabela. *option_name* é **varchar (35)**, sem nenhum padrão de NULL. *option_name* pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|table lock on bulk load|Quando desabilitado (o padrão), faz com que o processo de carregamento em massa em tabelas definidas pelo usuário obtenha bloqueio de linhas. Quando habilitado, faz com que os processos de carregamento em massa em tabelas definidas pelo usuário obtenham um bloqueio de atualização em massa.|  
|insert row lock|Não tem mais suporte.<br /><br /> Essa opção não tem nenhum efeito no comportamento de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e só é incluída para a compatibilidade de scripts e procedimentos existentes.|  
|text in row|Quando OFF ou 0 (desabilitado, o padrão), não altera o comportamento atual e não há nenhum BLOB na linha.<br /><br /> Quando especificado e @OptionValue está ativado (habilitado) ou um valor inteiro de 24 a 7000, novas cadeias de caracteres **Text**, **ntext**ou **Image** são armazenadas diretamente na linha de dados. Todo o BLOB existente (objeto binário grande: **texto**, **ntext**ou dados de **imagem** ) será alterado para texto no formato de linha quando o valor de blob for atualizado. Para obter mais informações, consulte Comentários.|  
|large value types out of row|1 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **XML** e grandes colunas de tipo definido pelo usuário (UDT) na tabela são armazenados fora da linha, com um ponteiro de 16 bytes para a raiz.<br /><br /> 0 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **XML** e valores de UDT grandes são armazenados diretamente na linha de dados, até um limite de 8000 bytes e desde que o valor possa caber no registro. Se o valor não se ajustar ao registro, um ponteiro será armazenado na linha e o restante será armazenado fora da linha no espaço de armazenamento de LOB. O valor padrão é 0.<br /><br /> O UDT (tipo definido pelo usuário) grande aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior. <br /><br /> Use a opção TEXTIMAGE_ON de [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) para especificar um local para armazenamento de tipos de dados grandes. |  
|formato de armazenamento vardecimal|**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br /><br /> Quando TRUE, ON ou 1, a tabela designada é habilitada para o formato de armazenamento vardecimal. Quando FALSE, OFF ou 0, a tabela designada não é habilitada para o formato de armazenamento vardecimal. O formato de armazenamento vardecimal só poderá ser habilitado quando o banco de dados tiver sido habilitado para o formato de armazenamento vardecimal usando [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md). No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, o formato de armazenamento **vardecimal** é preterido. Em vez disso, use compactação ROW. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md). O valor padrão é 0.|  
  
 [ @OptionValue =] '*valor*'  
 É se a *option_name* está habilitada (true, on ou 1) ou se está desabilitada (false, off ou 0). o *valor* é **varchar (12)**, sem padrão. o *valor* não diferencia maiúsculas de minúsculas.  
  
 Para a opção text in row, valores válidos são 0, ON, OFF ou um inteiro de 24 a 7000.  Quando o *valor* está ativado, o limite padrão é de 256 bytes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número de erro (falha)  
  
## <a name="remarks"></a>Comentários  
 Use sp_tableoption apenas para definir valores de opção para tabelas definidas pelo usuário. Para exibir as propriedades da tabela, use OBJECTPROPERTY ou consulta sys. Tables.  
  
 A opção text in row em sp_tableoption só pode ser habilitada ou desabilitada em tabelas que contêm colunas de texto. Se a tabela não tiver uma coluna de texto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro.  
  
 Quando a opção texto na linha está habilitada, o @OptionValue parâmetro permite que os usuários especifiquem o tamanho máximo a ser armazenado em uma linha para um blob. O padrão é 256 bytes, mas valores podem variar de 24 a 7000 bytes.  
  
 as cadeias de caracteres **Text**, **ntext**ou **Image** são armazenadas na linha de dados se as seguintes condições se aplicarem:  
  
-   A opção texto em linha está habilitada.  
  
-   O comprimento da cadeia de caracteres é menor que o limite especificado em @OptionValue  
  
-   Há bastante espaço disponível na linha de dados.  
  
 Quando as cadeias de caracteres de BLOB são armazenadas na linha de dados, a leitura e a gravação das cadeias de caracteres **Text**, **ntext**ou **Image** podem ser tão rápidas quanto a leitura ou a gravação de cadeias de caractere e binárias. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisa acessar páginas separadas para ler ou gravar a cadeia de caracteres BLOB.  
  
 Se uma cadeia de caracteres **Text**, **ntext**ou **Image** for maior do que o limite especificado ou o espaço disponível na linha, os ponteiros serão armazenados na linha em vez disso. As condições para armazenar as cadeias de caracteres BLOB na linha ainda assim se aplicam: deve haver espaço suficiente na linha de dados para conter os ponteiros.  
  
 As cadeias e ponteiros BLOB armazenados na linha de uma tabela são tratados de modo semelhante a cadeias de comprimento variável. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa só o número de bytes exigido para armazenar a cadeia de caracteres ou o ponteiro.  
  
 As cadeias BLOB existentes não são convertidas imediatamente, quando text in row é habilitada pela primeira vez. As cadeias só são convertidas quando são atualizadas. Da mesma forma, quando o limite da opção texto em linha for aumentado, as cadeias de caracteres **Text**, **ntext**ou **Image** já existentes na linha de dados não serão convertidas para aderir ao novo limite até a hora em que são atualizadas.  
  
> [!NOTE]  
>  Desabilitar a opção text in row ou reduzir o limite da opção exigirá a conversão de todas as BLOBs; assim, o processo pode ser longo, dependendo do número de cadeias BLOB que devem ser convertidas. A tabela é bloqueada durante o processo de conversão.  
  
 Uma variável de tabela, incluindo uma função que retorna uma variável de tabela, tem a opção text in row automaticamente habilitada com um limite padrão embutido de 256.  Essa opção não pode ser alterada.  
  
 A opção texto na linha dá suporte às funções TEXTPTR, WRITETEXT, UPDATETEXT e READTEXT. Os usuários podem ler partes de um BLOB com a função SUBSTRING(), mas devem se lembrar de que os ponteiros de texto na linha têm limites de número e duração diferentes de outros ponteiros de texto.  
  
 Para alterar uma tabela de formato de armazenamento vardecimal de volta ao formato de armazenamento decimal normal, o banco de dados deve estar em modo de recuperação SIMPLE. A alteração do modo de recuperação interromperá a cadeia de logs para efeito de backup, portanto, é necessário criar um backup de banco de dados completo depois de remover o formato de armazenamento vardecimal de uma tabela.  
  
 Se você estiver convertendo uma coluna de tipo de dados LOB (text, ntext ou image) existente em tipos de valor grande pequenos para médio (varchar (max), nvarchar (max) ou varbinary (max)) e a maioria das instruções não referenciar as colunas de tipo de valor grande em seu ambiente, considere alterar **large_value_types_out_of_row** para **1** para obter o desempenho ideal. Quando o valor da opção de **large_value_types_out_of_row** é alterado, os valores varchar (max), nvarchar (max), varbinary (max) e XML existentes não são convertidos imediatamente. O armazenamento da cadeia de caracteres é alterado conforme é atualizado subsequentemente. Qualquer novo valor inserido em uma tabela é armazenado de acordo com a opção da tabela em vigor. Para resultados imediatos, faça uma cópia dos dados e, em seguida, repopular a tabela depois de alterar a configuração de **large_value_types_out_of_row** ou atualizar cada coluna de tipos de valor grande de pequeno para médio para si mesma, para que o armazenamento das cadeias de caracteres seja alterado com a opção de tabela em vigor. Considere recompilar os índices na tabela após a atualização ou preencher novamente para condensar a tabela. 
    
  
## <a name="permissions"></a>Permissões  
 Para executar sp_tableoption é necessário ter permissão ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>a. Armazenando dados xml fora da linha  
 O exemplo a seguir especifica que os dados **XML** na `HumanResources.JobCandidate` tabela sejam armazenados fora da linha.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. Habilitando o formato de armazenamento vardecimal em uma tabela  
 O exemplo a seguir modifica a `Production.WorkOrderRouting` tabela para armazenar o `decimal` tipo de dados no `vardecimal` formato de armazenamento.  

```sql  
USE master;  
GO  
-- The database must be enabled for vardecimal storage format  
-- before a table can be enabled for vardecimal storage format  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON';  
GO  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'Production.WorkOrderRouting',   
   'vardecimal storage format', 'ON';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
