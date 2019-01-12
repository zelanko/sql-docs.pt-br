---
title: Histórico ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e3e491ccb659d8739cb93d72e0c923fce480015
ms.sourcegitcommit: 1f53b6a536ccffd701fc87e658ddac714f6da7a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54206432"
---
# <a name="ado-features-for-each-release"></a>Recursos para cada versão do ADO

Este tópico lista os novos recursos introduzidos por cada versão do ADO MD ADO e ADOX.

## <a name="ado-60"></a>ADO 6.0

 ADO 6.0 está incluído no Windows Vista, como parte do Windows Data Access Components (Windows DAC) 6.0. ADO 6.0 é funcionalmente equivalente ao ADO 2.8.

## <a name="ado-28"></a>ADO 2.8

 ADO 2.8 foi incluído no Windows XP e Windows Server 2003, como parte do Microsoft Data Access Components (MDAC) 2.8. Uma versão redistribuível do MDAC 2.8 também está disponível; Observe que esta versão redistribuível só deve ser instalado no Windows 2000. ADO 2.8 resolve muitas preocupações relacionadas à segurança:

 *Acesso de unidade de disco rígido não é permitido fora de uma zona confiável.*
No domínio cruzado que envolvem sites não confiáveis de script, as operações a seguir estão desabilitadas: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, e **Recordset.Open**, usado em conjunto com o **adCmdFile**  sinalizador ou com o Microsoft OLE DB provedor de persistência (MSPersist).

 **Recordset.Open** _,_ **Recordset.Save** _,_ **Stream.SaveToFile** _, e_ **Stream.LoadFromFile** _operam em arquivos físicos apenas._
Esses métodos agora verificam se os identificadores de arquivos apontam para apenas os arquivos físicos.

 **Recordset.ActiveCommand** _retornará um erro quando invocada a partir de uma página HTML/ASP._
Isso impede que o **comando** objeto sejam mal utilizadas.

 _O número de_**conjuntos de registros**_retornado por uma aninhada_**forma**_comando tem um limite superior._
Um comando de forma aninhada agora retorna um máximo de 512 **conjuntos de registros**. Isso significa que um **forma** comando não pode ser aninhado em qualquer profundidade. Em vez disso, a profundidade máxima de nível é 512, se cada comando resulta em uma única (filho) **conjunto de registros**. Se, em qualquer nível, uma **forma** comando retorna várias **conjuntos de registros**, o nível máximo de profundidade será menor que 512.

## <a name="ado-27"></a>ADO 2.7

 *suporte a plataformas de 64 bits* ADO 2.7 introduz o suporte para processadores de 64 bits.

## <a name="ado-26"></a>ADO 2.6

 **CubDef.GetSchemaObject**_método_ começando com o ADO 2.6, objetos do ADO MD podem ser recuperados usando nomes exclusivos, conforme especificado pelo [propriedade UniqueName (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md). Os nomes dos objetos pai não precisam ser conhecidos e pai coleções não precisam ser preenchidos para recuperar um objeto de esquema. Ver [método GetSchemaObject (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Comando fluxos* as **comando** objeto dá suporte a comandos no formato de fluxo como uma alternativa ao uso de **CommandText** propriedade. O [propriedade CommandStream (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) pode ser usado para especificar modelos XML ou diagramas de atualização como o **comando** de entrada com o Microsoft OLE DB Provider para SQL Server.

 **Dialeto**_propriedade_ [dialeto](../../ado/reference/ado-api/dialect-property.md) é uma nova propriedade que define a sintaxe e regras gerais que o provedor usa para analisar a cadeia de caracteres ou fluxo.

 **Command.Execute**_método_ o [método Execute](../../ado/reference/ado-api/execute-method-ado-command.md) do ADO **comando** objeto foi aperfeiçoado para usar fluxos de entrada e saída.

 *Campo statusvalues* se o usuário encontra um erro de DB_E_ERRORSOCCURRED ao modificar um **campo** de uma **conjunto de registros**, ADO preencherá o **Field.Status**propriedade com as informações de status apropriado para que o usuário terá de saber mais sobre o que deu errado. Ver [propriedade Status (campo ADO)](../../ado/reference/ado-api/status-property-ado-field.md).

 **NamedParameters**_propriedade_ [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) é uma nova propriedade de **comando** nomeado do objeto que indica que o provedor deve usar parâmetros.

 *Conjuntos de resultados em fluxos* ADO pode retornar conjuntos de resultados de uma fonte de dados em um **Stream**, em vez de uma **conjunto de registros** objeto. Usando a versão mais recente do Microsoft OLE DB Provider para SQL Server, você pode obter resultados XML do provedor executando uma consulta de "Para XML". Um **Stream** que recebe o conjunto de resultados pode ser aberto com um comando "Para XML" como a origem. Ver [recuperando conjuntos de resultados em fluxos](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *Conjunto de resultados de linha única* o ADO **registro** objeto agora pode ser aberto em uma cadeia de caracteres de comando ou **comando** objeto que retorna uma linha de dados do provedor. Isso resulta em melhor desempenho com provedores MDAC 2.6. Ver [(registro ADO) do método Open](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2.5

 **Registro** _objeto_ ADO 2.5 apresenta o **registro** objeto para representar e gerenciar uma linha de um **Recordset** ou um provedor de dados ou um objeto encapsulando um dados semi-estruturados, como um arquivo ou diretório.

 **Stream** _objeto_ ADO 2.5 também introduz o **Stream** objeto para representar um fluxo de dados de texto ou binárias.

 *Associação de URL* ADO 2.5 introduz o uso de uma URL, como uma alternativa para uma conexão comando e cadeia de caracteres de texto, para nomear objetos de repositório de dados. Uma URL pode ser usada com a existente **Conexão** e **conjunto de registros** objetos, bem como acontece com o novo **registro** e **Stream** objetos.

 *Provedores de dados que dão suporte a associação de URL* ADO 2.5 dá suporte a provedores OLE DB que reconhecem os esquemas de URL. Isso inclui o provedor OLE DB para publicação de Internet, que acessa o sistema de arquivos do Windows 2000 e reconhece o esquema HTTP existente.
