---
title: "Comparar tabelas replicadas para descobrir diferen&#231;as (Programa&#231;&#227;o de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "utilitário tablediff"
  - "comparando tabelas replicadas"
ms.assetid: cd253a17-0c85-42b4-912c-690169ebe799
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Comparar tabelas replicadas para descobrir diferen&#231;as (Programa&#231;&#227;o de replica&#231;&#227;o)
  A validação de artigo é usada para determinar se os dados publicados em artigos de tabelas no Publicador e no Assinante não são idênticos, pois isso poderia indicar não convergência. Para obter mais informações, consulte [Validar dados replicados](../../../relational-databases/replication/validate-replicated-data.md). Entretanto, a validação apenas retorna informações que passaram ou falharam e não fornece informação sobre qual é a diferença entre as tabelas de origem e de destino. O **tablediff** retorna do utilitário de prompt de comando detalhadas diferença informações entre duas tabelas e pode até mesmo gerar uma [!INCLUDE[tsql](../../../includes/tsql-md.md)] script para fazer a assinatura em convergência com dados no Editor.  
  
> [!NOTE]  
>  O **tablediff** utilitário só é suportado para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servidores.  
  
### Para comparar tabelas replicadas e encontrar diferenças usando tablediff  
  
1.  No prompt de comando em qualquer servidor em uma topologia de replicação, execute o [utilitário tablediff](../../../tools/tablediff-utility.md). Especifique os seguintes parâmetros:  
  
    -   **-sourceserver** - nome do servidor no qual os dados são conhecidos como correto, normalmente o publicador.  
  
    -   **-sourcedatabase** - nome do banco de dados que contém os dados corretos.  
  
    -   **-sourcetable** - nome da tabela de origem para o artigo que estão sendo comparado.  
  
    -   (Opcional) **-sourceschema** -proprietário do esquema da tabela de origem, caso contrário o esquema padrão.  
  
    -   (Opcional) **-sourceuser** e **- sourcepassword** ao usar a autenticação do SQL Server para se conectar ao Editor.  
  
        > [!IMPORTANT]  
        >  Quando possível, use a Autenticação do Windows. Se você precisa usar Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], solicite aos usuários para entrar com credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
    -   **-destinationserver** - nome do servidor no qual os dados estão sendo comparados, normalmente um assinante.  
  
    -   **-destinationdatabase** - nome de um banco de dados que estão sendo comparado.  
  
    -   **-destinationtable** - nome da tabela que estão sendo comparada.  
  
    -   (Opcional) **-destinationschema** -proprietário do esquema da tabela de destino, caso contrário o esquema padrão.  
  
    -   (Opcional) **-destinationuser** e **- destinationpassword** ao usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] autenticação para se conectar ao assinante.  
  
        > [!IMPORTANT]  
        >  Quando possível, use a Autenticação do Windows. Se você precisa usar Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], solicite aos usuários para entrar com credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
    -   (Opcional) Use **- c** para fazer uma comparação de nível de coluna.  
  
    -   (Opcional) Use **- q** para fazer uma rápida contagem - e somente de esquema de comparação de linha.  
  
    -   (Opcional) Especifique um nome de arquivo e caminho para **-o** para gerar os resultados em um arquivo.  
  
    -   (Opcional) Especifique uma tabela no banco de dados de assinatura para inserir resultados para **-et**. Se a tabela já existir, especifique **dt -** primeiro descartar a tabela.  
  
    -   (Opcional) Use **-f** para gerar um [!INCLUDE[tsql](../../../includes/tsql-md.md)] arquivo corrigir dados no assinante para que ele corresponda dados do publicador. Use **-df** para especificar o número de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções em cada arquivo.  
  
    -   (Opcional) Use **-rc** e **-ri** para especificar o número de vezes para repetir uma operação e o intervalo de repetição.  
  
    -   (Opcional) Use **-strict** para impor a comparação de esquema estrita entre tabelas de origem e destino.  
  
## Consulte também  
 [Validar dados no assinante](../../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  