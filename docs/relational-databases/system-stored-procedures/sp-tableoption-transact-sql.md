---
title: sp_tableoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_tableoption_TSQL
- sp_tableoption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_tableoption
ms.assetid: 0a57462c-1057-4c7d-bce3-852cc898341d
caps.latest.revision: 60
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 33027f15081102cca289923b858a4a960a1359e4
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sptableoption-transact-sql"></a>sp_tableoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define valores de opção para tabelas definidas pelo usuário. sp_tableoption pode ser usado para controlar o comportamento em linha de tabelas com **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml**, **texto**, **ntext**, **imagem**, ou colunas do tipo definido pelo usuário grande.  
  
> [!IMPORTANT]  
>  O recurso text in row será removido em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para armazenar dados de valor grande, é recomendável que você usar o **varchar (max)**, **nvarchar (max)** e **varbinary (max)** tipos de dados.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_tableoption [ @TableNamePattern = ] 'table'   
     , [ @OptionName = ] 'option_name'   
     ,[ @OptionValue =] 'value'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @TableNamePattern =] '*tabela*'  
 É o nome qualificado ou não qualificado de uma tabela de banco de dados definida pelo usuário. Se um nome de tabela totalmente qualificado, incluindo um nome de banco de dados, for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual. Não se pode definir opções de tabela para várias tabelas ao mesmo tempo. *tabela* é **nvarchar(776)**, sem padrão.  
  
 [ @OptionName =] '*option_name*'  
 É um nome de opção de tabela. *option_name* é **varchar (35)**, sem padrão de NULL. *option_name* pode ser um dos valores a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|table lock on bulk load|Quando desabilitado (o padrão), faz com que o processo de carregamento em massa em tabelas definidas pelo usuário obtenha bloqueio de linhas. Quando habilitado, faz com que os processos de carregamento em massa em tabelas definidas pelo usuário obtenham um bloqueio de atualização em massa.|  
|insert row lock|Não tem mais suporte.<br /><br /> Essa opção não tem nenhum efeito no comportamento de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e só é incluída para a compatibilidade de scripts e procedimentos existentes.|  
|text in row|Quando OFF ou 0 (desabilitado, o padrão), não altera o comportamento atual e não há nenhum BLOB na linha.<br /><br /> Quando especificado e @OptionValue está ON (habilitado) ou um valor inteiro de 24 a 7000, novas **texto**, **ntext**, ou **imagem** cadeias de caracteres são armazenadas diretamente na linha de dados. Todos os BLOBs existentes (objetos binários grandes: **texto**, **ntext**, ou **imagem** dados) serão alterados para texto em formato de linha quando o valor do BLOB for atualizado. Para obter mais informações, consulte Comentários.|  
|large value types out of row|1 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml** e colunas grandes tipo definido pelo usuário (UDT) na tabela são armazenadas fora de linha, com um ponteiro de 16 bytes para a raiz.<br /><br /> 0 = **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **xml** e valores UDT grandes são armazenados diretamente na linha de dados, até o limite de 8000 bytes e desde que o valor pode se ajustar no registro. Se o valor não se ajustar ao registro, um ponteiro será armazenado na linha e o restante será armazenado fora da linha no espaço de armazenamento de LOB. O valor padrão é 0.<br /><br /> O UDT (tipo definido pelo usuário) grande aplica-se a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. <br /><br /> Use a opção TEXTIMAGE_ON [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) para especificar um local para o armazenamento de tipos de dados grandes. |  
|formato de armazenamento vardecimal|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Quando TRUE, ON ou 1, a tabela designada é habilitada para o formato de armazenamento vardecimal. Quando FALSE, OFF ou 0, a tabela designada não é habilitada para o formato de armazenamento vardecimal. Formato de armazenamento vardecimal pode ser habilitado somente quando o banco de dados foi habilitado para o formato de armazenamento vardecimal usando [sp_db_vardecimal_storage_format](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md). Em [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, **vardecimal** o formato de armazenamento foi preterido. Em vez disso, use compactação ROW. Para obter mais informações, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md). O valor padrão é 0.|  
  
 [ @OptionValue =] '*valor*'  
 É se o *option_name* está habilitado (TRUE, no ou 1) ou desabilitado (FALSE, OFF ou 0). *valor* é **varchar(12)**, sem padrão. *valor* diferencia maiusculas de minúsculas.  
  
 Para a opção text in row, valores válidos são 0, ON, OFF ou um inteiro de 24 a 7000.  Quando *valor* for ON, o limite padrão é 256 bytes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número de erro (falha)  
  
## <a name="remarks"></a>Remarks  
 Use sp_tableoption apenas para definir valores de opção para tabelas definidas pelo usuário. Para exibir propriedades de tabela, use OBJECTPROPERTY.  
  
 A opção text in row em sp_tableoption só pode ser habilitada ou desabilitada em tabelas que contêm colunas de texto. Se a tabela não tiver uma coluna de texto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um erro.  
  
 Quando a opção text in row é habilitada, o @OptionValue parâmetro permite que os usuários especifiquem o tamanho máximo a ser armazenado em uma linha para um BLOB. O padrão é 256 bytes, mas valores podem variar de 24 a 7000 bytes.  
  
 **texto**, **ntext**, ou **imagem** cadeias de caracteres são armazenadas na linha de dados se as seguintes condições se aplicar:  
  
-   A opção texto em linha está habilitada.  
  
-   O comprimento da cadeia de caracteres é menor que o limite especificado em @OptionValue  
  
-   Há bastante espaço disponível na linha de dados.  
  
 Quando cadeias BLOB são armazenadas na linha de dados, ler e gravar o **texto**, **ntext**, ou **imagem** cadeias de caracteres podem ser tão rápidas quanto a leitura ou gravação de cadeias de caracteres e binárias. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisa acessar páginas separadas para ler ou gravar a cadeia de caracteres BLOB.  
  
 Se um **texto**, **ntext**, ou **imagem** cadeia de caracteres for maior que o limite especificado ou o espaço disponível na linha, ponteiros são armazenados na linha. As condições para armazenar as cadeias de caracteres BLOB na linha ainda assim se aplicam: deve haver espaço suficiente na linha de dados para conter os ponteiros.  
  
 As cadeias e ponteiros BLOB armazenados na linha de uma tabela são tratados de modo semelhante a cadeias de comprimento variável. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa só o número de bytes exigido para armazenar a cadeia de caracteres ou o ponteiro.  
  
 As cadeias BLOB existentes não são convertidas imediatamente, quando text in row é habilitada pela primeira vez. As cadeias só são convertidas quando são atualizadas. Da mesma forma, quando o texto no limite da opção de linha é aumentado, o **texto**, **ntext**, ou **imagem** cadeias de caracteres já na linha de dados não serão convertidas para aderir ao novo limite até o momento em que elas são atualizadas.  
  
> [!NOTE]  
>  Desabilitar a opção text in row ou reduzir o limite da opção exigirá a conversão de todas as BLOBs; assim, o processo pode ser longo, dependendo do número de cadeias BLOB que devem ser convertidas. A tabela é bloqueada durante o processo de conversão.  
  
 Uma variável de tabela, incluindo uma função que retorna uma variável de tabela, tem a opção text in row automaticamente habilitada com um limite padrão embutido de 256.  Essa opção não pode ser alterada.  
  
 A opção text in row oferece suporte as funções TEXTPTR, WRITETEXT, UPDATETEXT e READTEXT. Os usuários podem ler partes de um BLOB com a função SUBSTRING(), mas devem se lembrar de que os ponteiros de texto na linha têm limites de número e duração diferentes de outros ponteiros de texto.  
  
 Para alterar uma tabela de formato de armazenamento vardecimal de volta ao formato de armazenamento decimal normal, o banco de dados deve estar em modo de recuperação SIMPLE. A alteração do modo de recuperação interromperá a cadeia de logs para efeito de backup, portanto, é necessário criar um backup de banco de dados completo depois de remover o formato de armazenamento vardecimal de uma tabela.  
  
 Se você estiver convertendo uma existente dados tipo coluna LOB (text, ntext ou image) para tipos de valor grande de pequeno a médio porte (varchar (max), nvarchar (max), ou varbinary e maioria faz declarações não fazem referência as colunas de tipo de valor grande em seu ambiente, considere alterar **large_value_types_out_of_row** para **1** para obter o desempenho ideal. Quando o **large_value_types_out_of_row** valor de opção é alterado, existentes varchar (max), nvarchar (max), varbinary (max), e os valores de xml não são convertidos imediatamente. O armazenamento da cadeia de caracteres é alterado conforme é atualizado subsequentemente. Qualquer novo valor inserido em uma tabela é armazenado de acordo com a opção da tabela em vigor. Para resultados imediatos, ou faça uma cópia dos dados e, em seguida, preencha novamente a tabela depois de alterar o **large_value_types_out_of_row** configuração ou atualizar cada coluna de tipos de valor grande de pequeno a médio porte a mesmo para que o armazenamento da cadeias de caracteres é alterado com a opção de tabela em vigor. Considere recompilar os índices na tabela após a atualização ou preencher novamente para condensar a tabela. 
    
  
## <a name="permissions"></a>Permissões  
 Para executar sp_tableoption é necessário ter permissão ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-storing-xml-data-out-of-the-row"></a>A. Armazenando dados xml fora da linha  
 O exemplo a seguir especifica que o **xml** dados o `HumanResources.JobCandidate` tabela ser armazenada fora de linha.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_tableoption 'HumanResources.JobCandidate', 'large value types out of row', 1;  
```  
  
### <a name="b-enabling-vardecimal-storage-format-on-a-table"></a>B. Habilitando o formato de armazenamento vardecimal em uma tabela  
 O exemplo a seguir modifica o `Production.WorkOrderRouting` tabela para armazenar o `decimal` no tipo de dados a `vardecimal` o formato de armazenamento.  

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
  
## <a name="see-also"></a>Consulte também  
 [sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
