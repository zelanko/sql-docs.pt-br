---
title: Solucionar problemas de indexação de texto completo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- indexes [full-text search]
- troubleshooting [SQL Server], full-text search
- troubleshooting [full-text search]
ms.assetid: 964c43a8-5019-4179-82aa-63cd0ef592ef
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e408699252c30478036dc74a9ffe3a20e1e97c77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62716123"
---
# <a name="troubleshoot-full-text-indexing"></a>Solucionar problemas na indexação de texto completo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
     
##  <a name="failure"></a> Solucionar problemas de falhas na indexação de texto completo  
 Ao popular ou manter um índice de texto completo, o indexador de texto completo, pelas razões descritas a seguir, talvez falhe ao indexar uma ou mais linhas. Esses erros em nível de linha não impedem a conclusão da população. O indexador ignora essas linhas, o que significa que não é possível consultar seu conteúdo.  
  
 As falhas de indexação podem ocorrer quando:  
  
-   O indexador não consegue localizar ou carregar um filtro ou componente do separador de palavra. Essa falha pode ocorrer se a linha da tabela tiver um formato de documento ou conteúdo em idioma não registrado com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa falha também pode ocorrer se o componente do filtro ou o separador de palavra registrado não estava assinado ou se houve falha na verificação de assinatura ao carregar.  
  
-   Um componente, tal como um separador de palavras ou filtro, falha e retorna um erro ao indexador. Essa falha pode ocorrer se o documento a indexar estiver corrompido e o filtro não conseguir extrair seu texto. Essa falha também pode ocorrer quando um componente não puder tratar o conteúdo de uma única linha acima de um determinado tamanho, devido a limites de memória no host do daemon do filtro (fdhost.exe).  
  
 Para cada falha do nível de linha, o log de rastreamento contém detalhes da razão da falha. As contas de erro são resumidas no término de uma população completa ou com incremento.  
  
 Há outras falhas que podem impactar o próprio processo de indexação e impedir a conclusão da população:  
  
-   O índice de texto completo excede o limite para o número de linhas que podem ser contidas em um catálogo de texto completo.  
  
-   Um índice clusterizado ou um índice de chave de texto completo da tabela em indexação são alterados, descartados ou recriados.  
  
-   Uma falha no hardware ou disco corrompido resulta em corrupção do catálogo de texto completo.  
  
-   Um grupo de arquivo que contém a tabela cujo texto completo passa por indexação fica offline ou é do tipo somente leitura.  
  
 Examine o log de rastreamento ao término de qualquer operação significativa de população de índice de texto completo ou ao descobrir que a população não foi concluída.  
  
### <a name="unsigned-components"></a>Componentes não assinados  
 Por padrão, o indexador de texto completo requer os filtros e separadores de palavras que carrega ao assinar. Se não estiverem assinados, o que algumas vezes é o caso quando os componentes personalizados são instalados, é necessário configurar o indexador de texto completo para ignorar a verificação de assinatura.  
  
> [!IMPORTANT]  
>  Ignorar a verificação de assinatura torna menos segura a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Recomendamos assinar quaisquer componentes implementados ou garantir que os componentes que você adquirir estão assinados. Para obter informações sobre componentes de assinatura, veja [sp_fulltext_service &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md).  
  
  
##  <a name="state"></a> Índice de texto completo em estado inconsistente após o log de transações ser restaurado  
 Ao restaurar o log de transações de um banco de dados, é possível que apareça um aviso indicando que o índice de texto completo não está em um estado consistente. O motivo pelo qual isso ocorre é que o índice de texto completo de uma tabela foi modificado após ter sido feito o backup do banco de dados. Para trazer o índice de texto completo a um estado consistente, você deve executar uma população completa (rastreamento) na tabela. Para obter mais informações, veja [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
