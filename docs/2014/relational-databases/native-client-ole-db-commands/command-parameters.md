---
title: Parâmetros de comando | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- parameters [SQL Server Native Client]
- SQL Server Native Client OLE DB provider, parameters
- SQL Server Native Client OLE DB provider, commands
- parameters [SQL Server Native Client], OLE DB
- commands [OLE DB]
ms.assetid: 072ead49-ebaf-41eb-9a0f-613e9d990f26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 836f4cb41c8c2cf5b72dbbcf08b8154381a958cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62467342"
---
# <a name="command-parameters"></a>Parâmetros de comando
  Os parâmetros são marcados no texto do comando com o caractere de ponto de interrogação. Por exemplo, a seguinte instrução SQL é marcada para um único parâmetro de entrada:  
  
```  
{call SalesByCategory('Produce', ?)}  
```  
  
 Para melhorar o desempenho, reduzindo o tráfego [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de rede, o provedor de OLE DB de cliente nativo não deriva automaticamente as informações de parâmetro a menos que **ICommandWithParameters:: GetParameterInfo** ou **ICommandPrepare::P reparênteses** seja chamado antes de executar um comando. Isso significa que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não faz automaticamente:  
  
-   Verifique a exatidão do tipo de dados especificado com **ICommandWithParameters::SetParameterInfo**.  
  
-   Mapeie do DBTYPE especificado nas informações de associação do acessador para o tipo de dados correto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do parâmetro.  
  
 Os aplicativos receberão erros possíveis ou perda de precisão com um desses métodos, se especificarem tipos de dados não compatíveis com o tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do parâmetro.  
  
 Para garantir que isso não aconteça, o aplicativo deve:  
  
-   Garantir que *pwszDataSourceType* corresponda aos tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do parâmetro em caso de hard-coding de **ICommandWithParameters::SetParameterInfo**.  
  
-   Garantir que o valor DBTYPE associado ao parâmetro seja do mesmo tipo do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do parâmetro em caso de hard-coding de um acessador.  
  
-   Codifique o aplicativo para chamar **ICommandWithParameters::GetParameterInfo** de forma que o provedor possa obter os tipos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dos parâmetros dinamicamente. Observe que isso causa uma viagem de ida e volta na rede adicional até o servidor.  
  
> [!NOTE]  
>  O provedor não dá suporte à chamada a **ICommandWithParameters::GetParameterInfo** em nenhuma instrução UPDATE ou DELETE do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contenha uma cláusula FROM; em qualquer instrução SQL que dependa de uma subconsulta que contenha parâmetros; em instruções SQL que contenham marcadores de parâmetro em expressões de uma comparação, semelhança ou predicado quantificado; ou em consultas nas quais um dos parâmetros é um parâmetro de uma função. Ao processar um lote de instruções SQL, o provedor também não dá suporte à chamada a **ICommandWithParameters::GetParameterInfo** em marcadores de parâmetro nas instruções após a primeira instrução no lote. Não são permitidos comentários (/* \*/) no comando [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte a parâmetros de entrada nos comandos da instrução SQL. Nos comandos de chamada de procedimento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo oferece suporte a parâmetros de entrada, saída e entrada/saída. Os valores de parâmetro de saída são retornados para o aplicativo na execução (apenas se não houver nenhum conjunto de linhas retornado) ou quando todos os conjuntos de linhas retornados são esgotados pelo aplicativo. Para garantir a validade dos valores retornados, use **IMultipleResults** para forçar o consumo do conjunto de linhas.  
  
 Os nomes dos parâmetros de procedimento armazenado não precisam ser especificados em uma estrutura DBPARAMBINDINFO. Use NULL para o valor do membro *pwszName* para indicar que o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo deve ignorar o nome do parâmetro e usar apenas o ordinal especificado no membro *rgParamOrdinals* de **ICommandWithParameters:: SetParameterInfo**. Caso o texto do comando contenha parâmetros nomeados e sem-nome, todos os parâmetros sem-nome devem ser especificados antes de qualquer parâmetro nomeado.  
  
 Se o nome de um parâmetro de procedimento armazenado for especificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo verificará o nome para garantir que ele seja válido. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna um erro quando recebe um nome de parâmetro errado do consumidor.  
  
> [!NOTE]  
>  Para expor suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML e a UDT (tipos definidos pelo usuário), [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo implementa uma nova interface [ISSCommandWithParameters](../native-client-ole-db-interfaces/isscommandwithparameters-ole-db.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](commands.md)  
  
  
