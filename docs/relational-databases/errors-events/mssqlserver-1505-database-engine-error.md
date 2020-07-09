---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e30483860b6bdd29f485d90ef1145150910e0e31
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780970"
---
# <a name="mssqlserver_1505"></a>MSSQLSERVER_1505
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|1505|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DUP_KEY|  
|Texto da mensagem|A instrução CREATE UNIQUE INDEX foi encerrada porque foi encontrada uma chave duplicada para o nome de objeto '%.\*ls' e para o nome de índice '%.\*ls'.  O valor da chave duplicada é %ls.|  
  
## <a name="explanation"></a>Explicação  
Esse erro ocorre quando você tenta criar um índice exclusivo e mais de uma linha da tabela contém o valor duplicado especificado. Um índice exclusivo é criado quando você cria um índice e especifica a palavra-chave UNIQUE ou quando cria uma restrição UNIQUE. A tabela não pode conter linhas que tenham valores duplicados nas colunas definidas no índice ou na restrição.  
  
Considere os dados da seguinte tabela **Employee**:  
  
|LastName|Nome|JobTitle|HireDate|  
|------------|-------------|------------|------------|  
|Walters|Rob|Designer de ferramentas sênior|2004-11-19|  
|Brown|Kevin|Assistente de marketing|NULO|  
|Brown|Jo|Engenheiro de design|NULO|  
|Walters|Rob|Designer de ferramentas|2001-08-09|  
  
Não é possível criar um índice exclusivo com as combinações de coluna **LastName** ou **LastName** e **FirstName** devido aos valores duplicados nas linhas.  
  
Menos óbvia é a possibilidade de ocorrer uma violação de exclusividade na coluna **HireDate**. Para fins de indexação, valores NULL são comparados como iguais. Portanto, você não poderá criar um índice exclusivo ou uma restrição exclusiva se os valores de chave forem NULL em mais de uma linha. Considerando os dados acima, não é possível criar um índice exclusivo com base nas combinações de coluna **HireDate** ou **LastName** e **HireDate**.  
  
A mensagem de erro 1505 retorna a primeira linha que viola a restrição de exclusividade. Pode haver outras linhas duplicadas na tabela. Para encontrar todas as linhas duplicadas, consulte a tabela especificada e use as cláusulas GROUP BY e HAVING para reportar essas linhas. Por exemplo, a consulta a seguir retorna as linhas da tabela **Employee** que têm nomes e sobrenomes duplicados.  
  
SELECT LastName, FirstName, count(*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>Ação do usuário  
Considere as soluções descritas a seguir.  
  
-   Adicione ou remova colunas na definição do índice ou da restrição para criar uma composição exclusiva. No exemplo anterior, adicionar uma coluna **MiddleName** à definição do índice ou da restrição pode resolver o problema de duplicação.  
  
-   Selecione colunas definidas como NOT NULL quando escolher colunas para um índice exclusivo ou para uma restrição exclusiva. Isso elimina a possibilidade de ocorrer uma violação de exclusividade gerada quando mais de uma linha contiver NULL nos valores de chave.  
  
-   Se os valores duplicados forem o resultado de erros de entrada de dados, corrija os dados manualmente e, em seguida, crie o índice ou a restrição. Para obter informações sobre como remover linhas duplicadas de uma tabela, veja o artigo 139444 da base de dados de conhecimento: [Como remover linhas duplicadas de uma tabela no SQL Server](https://support.microsoft.com/kb/139444).  
  
## <a name="see-also"></a>Consulte Também  
[CREATE INDEX &#40;Transact-SQL&#41;](~/t-sql/statements/create-index-transact-sql.md)  
[Criar índices exclusivos](~/relational-databases/indexes/create-unique-indexes.md)  
[Criar restrições exclusivas](~/relational-databases/tables/create-unique-constraints.md)  
  
