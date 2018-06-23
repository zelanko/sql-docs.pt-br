---
title: Propriedades de sequência (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.sequence.general.f1
ms.assetid: 0187f413-cdf0-48a2-b2e6-9b3578cd5811
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c71b31282ac1ed242c6b8f35adeff24cbc9ddf9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010396"
---
# <a name="sequence-properties-general-page"></a>Propriedades da Sequência (página Geral)
  Cria um objeto de sequência e especifica suas propriedades. Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com a especificação com a qual a sequência foi criada. A sequência de valores numéricos é gerada em ordem crescente ou decrescente em um intervalo definido e pode ser configurada para reiniciar (em um ciclo) quando se esgotar. As sequências, ao contrário de colunas de identidade, não são associadas a tabelas específicas. Os aplicativos fazem referência a um objeto de sequência para recuperar seu próximo valor. A relação entre sequências e tabelas é controlada pelo aplicativo. Os aplicativos de usuário podem referenciar um objeto de sequência e coordenar os valores nas várias linhas e tabelas.  
  
 Ao contrário de valores de colunas de identidade que são gerados no momento da inserção, um aplicativo pode obter o próximo número de sequência sem inserir a linha por meio da chamada da [função NEXT VALUE FOR](/sql/t-sql/functions/next-value-for-transact-sql). Use [sp_sequence_get_range](/sql/relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql) para obter vários números de sequência de uma vez.  
  
 Para obter informações e cenários que usam **CREATE SEQUENCE** e a função **NEXT VALUE FOR** , consulte [Números de sequência](sequence-numbers.md).  
  
 Essa página é acessada de duas maneiras: com um clique com o botão direito do mouse em **Sequências** no Pesquisador de Objetos e com um clique em **Nova Sequência**ou com um clique com o botão direito do mouse em uma sequência existente e um clique em **Propriedades**. Quando você clica com o botão direito do mouse em uma sequência existente e clica em **Propriedades**, as opções não são editáveis. Para alterar as opções de sequência, use a instrução [ALTER SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-sequence-transact-sql) ou remova e crie novamente o objeto de sequência.  
  
## <a name="options"></a>Opções  
 **Nome da sequência**  
 Digite o nome da sequência aqui.  
  
 **Esquema da sequência**  
 Especifique o esquema que possuirá esta sequência.  
  
 **Tipo de dados**  
 Uma sequência pode ser definida como qualquer tipo de inteiro. Isso inclui:  
  
|Tipo de dados|Intervalo|  
|---------------|-----------|  
|`tinyint`|0 a 255|  
|`smallint`|-32.768 a 32.767|  
|`int`|-2.147.483.648 a 2.147.483.647|  
|`bigint`|-9.223.372.036.854.775.808 a 9.223.372.036.854.775.807|  
  
-   `decimal` ou `numeric` com uma escala de 0.  
  
-   Qualquer tipo de dados definido pelo usuário (tipo de alias) que seja baseado em um destes tipos.  
  
 **Precisão**  
 Para tipos de dados `decimal` ou `numeric`, especifique a precisão. (A escala é sempre 0.)  
  
 **Iniciar com valor**  
 O primeiro valor que será retornado pelo objeto de sequência. O valor **START** deve ser um valor que seja menor ou igual ao valor máximo e maior ou igual ao valor mínimo do objeto de sequência. O valor de início padrão para um novo objeto de sequência é o valor mínimo para um objeto de sequência e o valor máximo de um objeto de sequência decrescente.  
  
 **Incrementar por**  
 O valor usado para incrementar (ou decrementar, se negativo) o valor do objeto de sequência para cada chamada da função **NEXT VALUE FOR** . Se o incremento for um valor negativo, o objeto de sequência será decrescente; caso contrário, será crescente. O incremento não pode ser 0.  
  
 **Valor mínimo**  
 Especifica os limites do objeto de sequência. O valor mínimo padrão de um novo objeto de sequência é o valor mínimo do tipo de dados do objeto de sequência. Isso é zero para o `tinyint` tipo de dados e um número negativo para todos os outros tipos de dados.  
  
 **Valor máximo**  
 Especifica os limites do objeto de sequência. O valor máximo padrão para um novo objeto de sequência é o valor máximo do tipo de dados do objeto de sequência.  
  
 **A sequência do ciclo será reiniciada ao atingir o limite**  
 Selecione para permitir que o objeto de sequência reinicie a partir do valor mínimo (ou do valor máximo para objetos de sequência decrescente) quando o valor mínimo ou máximo for excedido.  
  
> [!NOTE]  
>  O ciclo não é reiniciado a partir do valor inicial, mas a partir do valor mínimo/máximo.  
  
 **Opções de cache**  
 A criação de um cache de valores de sequência pode aumentar o desempenho de aplicativos que usam objetos de sequência por meio da minimização do número de E/S de disco necessárias para criar números de sequência.  
  
-   Tamanho do cache padrão: o [!INCLUDE[ssDE](../../includes/ssde-md.md)] selecionará um tamanho, porém, os usuários não devem confiar que essa seleção seja consistente. [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode alterar o método de cálculo do tamanho do cache sem aviso prévio.  
  
-   Sem cache: o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não armazenará os números de sequência em cache.  
  
-   Cache com tamanho - O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazenará valores de sequência em cache. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controla o valor atual e o número de valores deixados no cache. Portanto, a quantidade de memória necessária para armazenar o cache sempre é duas instâncias do tipo de dados do objeto de sequência  
  
 Quando criado com a opção CACHE, um desligamento inesperado, como uma deficiência de energia, pode perder os números de sequência no cache.  
  
 Para obter informações adicionais sobre as opções de sequência de criação, consulte [CREATE SEQUENCE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-sequence-transact-sql).  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **CREATE SEQUENCE**, **ALTER**ou **CONTROL** no SCHEMA.  
  
## <a name="see-also"></a>Consulte também  
 [sys.sequences &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sequences-transact-sql)  
  
  
