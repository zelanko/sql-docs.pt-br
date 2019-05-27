---
title: Convenções da sintaxe Transact-SQL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- sql13.TSQLExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- conventions [SQL Server]
- Applies to section in Transact-SQL topics
- code example conventions [SQL Server]
- objects [SQL Server], names
- code [SQL Server], conventions
- multipart names [SQL Server]
- Transact-SQL syntax conventions
- syntax conventions [SQL Server]
- code [SQL Server]
- Transact-SQL
- naming conventions [SQL Server]
- syntax [SQL Server], Transact-SQL
ms.assetid: 35fbcf7f-8b55-46cd-a957-9b8c7b311241
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edc4bd43b27235a35b6c8ed213e2925523015fde
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65981457"
---
# <a name="transact-sql-syntax-conventions-transact-sql"></a>Convenções da sintaxe Transact-SQL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

A tabela a seguir lista e descreve as convenções usadas nos diagramas de sintaxe na Referência [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
|Convenção|Usado para|  
|----------------|--------------|  
|UPPERCASE|Palavras-chave [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|_italic_|Parâmetros de sintaxe [!INCLUDE[tsql](../../includes/tsql-md.md)] fornecidos pelo usuário.|  
|**bold**|Digite os nomes dos bancos de dados, nomes de tabela, nomes de coluna, nomes de índices, procedimentos armazenados, utilitários, nomes de tipo de dados e texto exatamente como exibidos.|  
|underline|Indica o valor padrão aplicado quando a cláusula que contém o valor sublinhado é omitida da instrução.|  
|&#124; (barra vertical)|Separa itens de sintaxe que se encontram entre colchetes ou entre chaves. Você pode usar só um dos itens.|  
|`[ ]` (colchetes)|Itens de sintaxe opcionais. Não digite os colchetes.|  
|{ } (chaves)|Itens de sintaxe exigidos. Não digite os colchetes.|  
|[ **,** ..._n_]|Indica que o item precedente pode ser repetido _n_ vezes. As ocorrências são separadas por vírgulas.|  
|[..._n_]|Indica que o item precedente pode ser repetido _n_ vezes. As ocorrências são separadas por espaços em branco.|  
|;|Terminador de instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Embora o ponto e vírgula não seja necessário para a maioria das instruções nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele será necessário em uma versão futura.|  
|\<label> ::=|O nome de um bloco de sintaxe. Use essa convenção para agrupar e rotular seções de sintaxe extensa ou uma unidade de sintaxe que pode ser usada em mais de um local dentro de uma instrução. Cada local no qual o bloco de sintaxe pode ser usado é indicado com o rótulo entre divisas: \<label>.<br /><br /> Um conjunto é uma coleção de expressões, por exemplo, \<grouping set>, e uma lista é uma coleção de conjuntos, por exemplo, \<composite element list>.|  
  
## <a name="multipart-names"></a>Nomes de partes múltiplas  
A menos que especificado de outra forma, todas as referências [!INCLUDE[tsql](../../includes/tsql-md.md)] ao nome de um objeto de banco de dados podem ser um nome de quatro partes, do seguinte modo:  
  
_servidor\_nome_.[_bancodedados\_nome_].[_esquema\_nome_]._objeto\_nome_  
  
| _bancodedados\_nome_.[_esquema\_nome_]._objeto\_nome_  
 
| _esquema\_nome_._objeto\_nome_  
  
| _object\_name_  
  
_server\_name_  
Especifica um nome de servidor vinculado ou remoto.  
  
_bancodedados\_nome_  
Especifica o nome de um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o objeto reside em uma instância local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o objeto está em um servidor vinculado, *database_name* especifica um catálogo OLE DB.  
  
_esquema\_nome_  
Especifica o nome do esquema que contém o objeto, se o objeto estiver em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o objeto está em um servidor vinculado, *schema_name* especifica um nome de esquema OLE DB.  
  
_objeto\_nome_  
Refere-se ao nome do objeto.  
  
Quando se refere a um objeto específico, nem sempre é preciso especificar o servidor, o banco de dados e o esquema para que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] identifique o objeto. Porém, se o objeto não puder ser encontrado, um erro será retornado.  
  
> [!NOTE]  
> Para evitar erros de resolução de nome, recomendamos especificar o nome de esquema sempre que você especificar um objeto no escopo do esquema.  
  
Para omitir nós intermediários, use pontos para indicar essas posições. A tabela a seguir mostra os formatos válidos de nomes de objetos.  
  
|Formato de referência de objeto|Descrição|  
|-----------------------------|-----------------|  
|_servidor_._bancodedados_._esquema_._objeto_|Nome de quatro partes.|  
|_servidor_._bancodedados_.._objeto_|O nome do esquema é omitido.|  
|_servidor_.._esquema_._objeto_|O nome do banco de dados é omitido.|  
|_servidor_..._objeto_|Os nomes do banco de dados e do esquema são omitidos.|  
|_bancodedados_._esquema_._objeto_|O nome do servidor é omitido.|  
|_bancodedados_.._objeto_|Os nomes do servidor e do esquema são omitidos.|  
|_esquema_._objeto_|Os nomes do servidor e do banco de dados são omitidos.|  
|_object_|Os nomes do servidor, do banco de dados e do esquema são omitidos.|  
  
## <a name="code-example-conventions"></a>Convenções de exemplo de código  
Salvo indicação em contrário, os exemplos fornecidos na Referência do [!INCLUDE[tsql](../../includes/tsql-md.md)] foram testados usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e suas configurações padrão para as seguintes opções:  
  
-   ANSI_NULLS  
-   ANSI_NULL_DFLT_ON  
-   ANSI_PADDING  
-   ANSI_WARNINGS  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER  
  
A maioria dos exemplos de código na Referência do [!INCLUDE[tsql](../../includes/tsql-md.md)] foi testada em servidores executando uma ordem de classificação com diferenciação de maiúsculas e minúsculas. Os servidores de teste executaram, normalmente, a página de código ANSI/ISO 1252.  
  
Muitos exemplos de código incluem um prefixo em constantes de cadeia de caracteres Unicode com a letra **N**. Sem o prefixo **N**, a cadeia de caracteres é convertida na página de código padrão do banco de dados. Essa página de código padrão pode não reconhecer certos caracteres.  
  
## <a name="applies-to-references"></a>Referências de "Aplica-se a"  
A referência [!INCLUDE[tsql](../../includes/tsql-md.md)] inclui artigos relacionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], (do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)].   

Existe uma seção na parte superior de cada artigo indicando quais produtos são compatíveis com o assunto do artigo. Se um produto for omitido, o recurso descrito pelo artigo não estará disponível para esse produto. Por exemplo, os grupos de disponibilidade foram introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. O artigo **CRIAR GRUPO DE DISPONIBILIDADE** indica que ele se aplica ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), pois não se aplica ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], ao [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e nem ao [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
O assunto geral do artigo pode ser usado em um produto, mas em alguns casos não há suporte para todos os argumentos. Por exemplo, os usuários do banco de dados independente foram introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Use a instrução **CREATE USER** em qualquer produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no entanto, a sintaxe **WITH PASSWORD** não pode ser usada com versões anteriores. As seções **Aplica-se a** adicionais são inseridas em descrições de argumento apropriadas no corpo do artigo.  
  
## <a name="see-also"></a>Consulte Também  
[Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/transact-sql-reference-database-engine.md)    
[Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)      
[Problemas de design do Transact-SQL](https://msdn.microsoft.com/library/dd193411.aspx)    
[Problemas de nomenclatura do Transact-SQL](https://msdn.microsoft.com/library/dd193246.aspx)        
[Problemas de desempenho do Transact-SQL](https://msdn.microsoft.com/library/dd172117.aspx)    


