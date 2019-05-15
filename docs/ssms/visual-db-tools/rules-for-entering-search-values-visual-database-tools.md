---
title: Regras para inserção de valores de pesquisa (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], searches
- date searches
- dates [SQL Server], searches
- embedding apostrophes [SQL Server]
- logical value searches [SQL Server]
- case-sensitive search matches
- search criteria [SQL Server], rules
- text value searches [SQL Server]
- numeric value searches [SQL Server]
ms.assetid: 3c8134b7-83f4-41b4-99c8-e3949a685ff5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 76cc525bbab351cb440d1a1078ef008205b7be94
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106294"
---
# <a name="rules-for-entering-search-values-visual-database-tools"></a>Regras para inserção de valores de pesquisa (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Este tópico discute as convenções que devem ser usadas para inserir os seguintes tipos de valores literais em um critério de pesquisa:  
  
-   Valores de texto  
  
-   Valores numéricos  
  
-   Datas  
  
-   Valores lógicos  
  
> [!NOTE]  
> As informações contidas neste tópico derivam de regras para o SQL-92 padrão. No entanto, cada banco de dados pode implementar o SQL à sua própria maneira. Assim, as diretrizes aqui fornecidas talvez não se apliquem a todos os casos. Se você tiver dúvidas sobre como inserir valores de pesquisa em um banco de dados específico, recorra à documentação do banco de dados em uso.  
  
## <a name="searching-on-text-values"></a>Pesquisando valores de texto  
As diretrizes a seguir são aplicadas quando se inserem valores de texto em critérios de pesquisa:  
  
-   **Aspas** Coloque valores de texto entre aspas simples, assim como neste exemplo de sobrenome:  
  
    ```  
    'Smith'  
    ```  
  
    Ao inserir um critério de pesquisa no [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), basta digitar o valor de texto e o Designer de Consultas e Exibição colocará automaticamente o valor entre aspas simples.  
  
    > [!NOTE]  
    > Em alguns bancos de dados, os termos entre aspas simples são interpretados como valores literais, enquanto os termos entre aspas duplas são interpretados como objetos de banco de dados, por exemplo, referências de coluna ou tabela. Portanto, embora o Designer de Consulta e Exibição possa aceitar os termos com aspas duplas, ele poderá interpretá-los diferentemente do esperado.  
  
-   **Incorporação de Apóstrofos** Se os dados sendo pesquisados contiverem uma aspa única (apóstrofo), insira duas aspas simples para indicar que você entende a aspa única como valor literal e não como delimitador. Por exemplo, a condição a seguir pesquisa o valor "Caminho de Swann":  
  
    ```  
    ='Swann''s Way'  
    ```  
  
-   **Limites de comprimento** Não exceda o comprimento máximo da instrução SQL do banco de dados quando inserir longas cadeias de caracteres.  
  
-   **Diferenciação de maiúsculas e minúsculas** Siga as regras de diferenciação de maiúsculas e minúsculas do banco de dados em uso. O banco de dados em uso determina se as pesquisas de texto diferenciam maiúsculas e minúsculas. Por exemplo, alguns bancos de dados interpretam o operador "=" como significando uma correspondência exata entre maiúsculas e minúsculas, mas outros permitem correspondências de qualquer combinação de caracteres maiúsculos e minúsculos.  
  
    Se você não tiver certeza se o banco de dados utiliza pesquisa com diferenciação de maiúsculas e minúsculas ou não, use as funções UPPER ou LOWER no critério de pesquisa para converter as maiúsculas e minúsculas dos dados de pesquisa, como ilustrado no exemplo abaixo:  
  
    ```  
    WHERE UPPER(lname) = 'SMITH'  
    ```  
  
## <a name="searching-on-numeric-values"></a>Pesquisando valores numéricos  
As diretrizes a seguir são aplicada quando se inserem valores numéricos em critérios de pesquisa:  
  
-   **Aspas** Não inclua números entre aspas.  
  
-   **Caracteres não numéricos** Não inclua caracteres não numéricos, exceto o separador decimal (conforme definido na caixa de diálogo **Configurações Regionais** do Painel de Controle do Windows) e o sinal negativo (-). Não inclua símbolos que agrupam dígitos (como uma vírgula entre os milhares) ou símbolos de moeda.  
  
-   **Marcas decimais** Se você estiver digitando números inteiros, poderá incluir uma marca decimal, caso o valor pesquisado seja número inteiro ou real.  
  
-   **Notação científica** Você pode inserir números muito grandes ou muito pequenos que usam notação científica, como neste exemplo:  
  
    ```  
    > 1.23456e-9  
    ```  
  
## <a name="searching-on-dates"></a>Pesquisando datas  
O formato usado para inserir datas depende do banco de dados que você está usando e do painel do Designer de Consulta e Exibição em que está inserindo as datas.  
  
> [!NOTE]  
> Se você não souber qual é o formato usado pela fonte de dados, digite uma data na coluna de filtro do Painel de critérios em qualquer formato que lhe seja familiar. O Designer converterá a maioria dessas inserções para o formato apropriado.  
  
O Designer de Consulta e Exibição trabalha com os seguintes formatos de data:  
  
-   **Específico de localidade** Formato especificado para datas na caixa de diálogo **Propriedades de Configurações Regionais do Windows** .  
  
-   **Específico de banco de dados** Qualquer formato entendido pelo banco de dados.  
  
-   **Padrão de data ANSI** Formato que usa chaves; o marcador 'd' para designar a data e uma cadeia de caracteres de data, como no exemplo a seguir:  
  
    ```  
    { d '1990-12-31' }  
    ```  
  
-   **Data e hora padrão ANSI** Semelhante à data padrão ANSI, porém usando 'ts' em vez de 'd' e adicionando horas, minutos e segundos à data (utiliza o formato de dia de 24 horas), como neste exemplo de 31 de dezembro de 1990:  
  
    ```  
    { ts '1990-12-31 00:00:00' }  
    ```  
  
    Em geral, o formato de data padrão ANSI é usado em bancos de dados que representam datas usando um tipo de dados de data real. Por outro lado, o formato de data e hora é usado em bancos de dados que dão suporte ao tipo de dados de data e hora.  
  
A tabela a seguir resume o formato de data que pode ser usado em diferentes painéis do Designer de Consulta e Exibição.  
  
|**Painel**|**Formato de data**|  
|------------|-------------------|  
|Critérios|Padrão ANSI específico de Banco de dados e específico de localidade<br /><br />As datas inseridas no [Painel Critérios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md) são convertidas em formato compatível com banco de dados no painel SQL.|  
|SQL|Padrão ANSI específico de banco de dados|  
|Resultados|Específico de localidade|  
  
## <a name="searching-on-logical-values"></a>Pesquisando valores lógicos  
O formato de dados lógicos varia entre os bancos de dados. Muito frequentemente, um valor False é armazenado como zero (0). Um valor True é armazenado com mais frequência como 1 e ocasionalmente como -1. As diretrizes a seguir são aplicadas quando se inserem valores lógicos em critérios de pesquisa:  
  
-   Para pesquisar um valor False, use um zero, como no exemplo abaixo:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 0  
    ```  
  
-   Se você não tiver certeza do formato a ser usado durante a pesquisa de um valor True, tente usar 1, como no exemplo a seguir:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract = 1  
    ```  
  
-   Como alternativa, você pode ampliar o escopo da pesquisa procurando qualquer valor diferente de zero, como neste exemplo:  
  
    ```  
    SELECT * FROM authors  
    WHERE contract <> 0  
    ```  
  
## <a name="see-also"></a>Consulte Também  
[Especificar critérios de pesquisa &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
