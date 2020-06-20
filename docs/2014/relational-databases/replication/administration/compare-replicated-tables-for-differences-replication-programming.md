---
title: Comparar tabelas replicadas para descobrir diferenças (Programação de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- tablediff utility
- comparing replicated tables
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a7d6315a8d8237effe5ae888d303e3aab0dcef1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038405"
---
# <a name="compare-replicated-tables-for-differences-replication-programming"></a>Comparar tabelas replicadas para descobrir diferenças (Programação de replicação)
  A validação de artigo é usada para determinar se os dados publicados em artigos de tabelas no Publicador e no Assinante não são idênticos, pois isso poderia indicar não convergência. Para obter mais informações, consulte [Validar os dados replicados](../validate-data-at-the-subscriber.md). Entretanto, a validação apenas retorna informações que passaram ou falharam e não fornece informação sobre qual é a diferença entre as tabelas de origem e de destino. O utilitário de prompt de comando **tablediff** retorna informações detalhadas sobre a diferença entre duas tabelas e pode até gerar um script [!INCLUDE[tsql](../../../includes/tsql-md.md)] para fazer convergir a assinatura com os dados no Publicador.  
  
> [!NOTE]  
>  O utilitário **tablediff** tem suporte apenas nos servidores [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
### <a name="to-compare-replicated-tables-for-differences-using-tablediff"></a>Para comparar tabelas replicadas e encontrar diferenças usando tablediff  
  
1.  No prompt de comando de qualquer servidor em uma topologia de replicação, execute o [tablediff Utility](../../../tools/tablediff-utility.md). Especifique os seguintes parâmetros:  
  
    -   **- sourceserver** - nome do servidor no qual os dados são os corretos, normalmente o Publicador.  
  
    -   **- sourcedatabase** - nome do banco de dados que contém os dados corretos.  
  
    -   **- sourcetable** - nome da tabela de origem do artigo que é comparado.  
  
    -   (Opcional) **- sourceschema** - proprietário do esquema da tabela de origem, se não for o esquema padrão.  
  
    -   (Opcional) **-sourceuser** e **-sourcepassword** quando usar a Autenticação do SQL Server para se conectar ao Publicador.  
  
        > [!IMPORTANT]  
        >  Quando possível, use a Autenticação do Windows. Se você precisa usar Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , solicite aos usuários para entrar com credenciais de segurança em runtime. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
    -   **- destinationserver** - nome do servidor no qual os dados estão sendo comparados, normalmente um Assinante.  
  
    -   **- destinationdatabase** - nome do banco de dados que é comparado.  
  
    -   **- destinationtable** - nome da tabela que é comparada.  
  
    -   (Opcional) **- destinationschema** - proprietário do esquema da tabela de destino, se não for o esquema padrão.  
  
    -   (Opcional) **- destinationuser** e **- destinationpassword** ao usar Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para conectar ao Assinante.  
  
        > [!IMPORTANT]  
        >  Quando possível, use a Autenticação do Windows. Se você precisa usar Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , solicite aos usuários para entrar com credenciais de segurança em runtime. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
    -   (Opcional) Use **- c** para fazer uma comparação no nível de coluna.  
  
    -   (Opcional) Use **- q** para fazer uma rápida contagem somente de linhas e esquema.  
  
    -   (Opcional) Especifique um nome de arquivo e caminho para **- o** para a saída dos resultados em um arquivo.  
  
    -   (Opcional) Especifique uma tabela no banco de dados de assinatura para inserir resultados de **- et**. Se a tabela já existir, especifique **- dt** para cancelar primeiro a tabela.  
  
    -   (Opcional) Use **-f** para gerar um arquivo [!INCLUDE[tsql](../../../includes/tsql-md.md)] para corrigir os dados no Assinante e corresponderem aos dados do Publicador. Use **- df** para especificar o número de instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] em cada arquivo.  
  
    -   (Opcional) Use **- rc** e **- ri** para especificar o número de horas para repetir uma operação e o intervalo de repetição.  
  
    -   (Opcional) Use **- strict** para impor uma comparação de esquema estrita entre tabelas de origem e destino.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar dados no assinante](../validate-data-at-the-subscriber.md)  
  
  
