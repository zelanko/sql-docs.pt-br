---
title: Sobre o controle de alterações (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data changes [SQL Server]
- tracking data changes [SQL Server]
- change tracking [SQL Server], about change tracking
- change tracking [SQL Server]
- data [SQL Server], changing
ms.assetid: 5e0ef05a-8317-4c98-be20-b19d4cd78f12
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e2013a604c517ae93ee17640013e2260f50cf28e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62670910"
---
# <a name="about-change-tracking-sql-server"></a>Sobre o controle de alterações (SQL Server)
  O controle de alterações é uma solução leve que fornece um mecanismo de controle de alterações eficiente para aplicativos. Em geral, para permitir que os aplicativos consultassem as alterações nos dados de um banco de dados e acessassem as informações relacionadas às alterações, os desenvolvedores de aplicativos precisavam implementar mecanismos personalizados de controle de alterações. A criação desses mecanismos geralmente envolvia muito trabalho e frequentemente envolvida usando uma combinação de gatilhos `timestamp` , colunas, novas tabelas para armazenar informações de rastreamento e processos de limpeza personalizados.  
  
 Tipos distintos de aplicativos têm requisitos diferentes quanto à quantidade de informações que precisam sobre as alterações. Os aplicativos podem usar o controle de alterações para responder às seguintes perguntas sobre as alterações feitas na tabela de um usuário:  
  
-   Que linhas da tabela de um usuário foram alteradas?  
  
    -   Só é necessário o fato de que uma linha foi alterada, e não quantas vezes ela foi alterada ou os valores das alterações intermediárias.  
  
    -   Os últimos dados podem ser obtidos diretamente da tabela que está sendo controlada.  
  
-   Uma linha foi alterada?  
  
    -   O fato de que uma linha foi alterada e as informações sobre a alteração devem estar disponíveis e serem registrados no momento em que a alteração foi feita na mesma transação.  
  
> [!NOTE]  
>  Se um aplicativo precisar de informações sobre todas as alterações feitas e os valores intermediários dos dados alterados, talvez seja adequado usar o Change Data Capture, em vez do controle de alterações. Para obter mais informações, veja [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../track-changes/about-change-data-capture-sql-server.md).  
  
## <a name="one-way-and-two-way-synchronization-applications"></a>Aplicativos de sincronização unidirecional e bidirecional  
 Os aplicativos que precisam sincronizar dados com uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] devem poder consultar alterações. O controle de alterações pode ser usado como uma base para aplicativos de sincronização unidirecional e bidirecional.  
  
### <a name="one-way-synchronization-applications"></a>Aplicativos de sincronização unidirecional  
 É possível criar aplicativos de sincronização unidirecional, como um aplicativo cliente ou de cache de camada intermediária, que usem o controle de alterações. Como mostra a ilustração a seguir, um aplicativo em cache exige que os dados sejam armazenados no [!INCLUDE[ssDE](../../includes/ssde-md.md)] e armazenados em cache em outros armazenamentos de dados. O aplicativo deve ser capaz de manter o cache atualizado com as alterações feitas nas tabelas do banco de dados. Não há nenhuma alteração para devolver ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 ![Mostra aplicativos de sincronização unidirecional](../../database-engine/media/one-waysync.gif "Mostra aplicativos de sincronização unidirecional")  
  
### <a name="two-way-synchronization-applications"></a>Aplicativos de sincronização bidirecional  
 Também é possível criar aplicativos de sincronização bidirecional que usem o controle de alterações. Neste cenário, os dados em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] são sincronizados com um ou mais repositórios de dados. Os dados nesses repositórios podem ser atualizados, e as alterações devem ser sincronizadas novamente com o [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 ![Mostra aplicativos de sincronização bidirecional](../../database-engine/media/two-waysync.gif "Mostra aplicativos de sincronização bidirecional")  
  
 Um bom exemplo de aplicativo de sincronização bidirecional é um aplicativo ocasionalmente conectado. Nesse tipo de aplicativo, um aplicativo cliente consulta e atualiza um repositório local. Quando houver uma conexão disponível entre um cliente e um servidor, o aplicativo será sincronizado com um servidor, e os fluxos de dados alterados ocorrerão nas duas direções.  
  
 Os aplicativos de sincronização bidirecional devem ser capazes de detectar conflitos. Ocorrerá um conflito se os mesmos dados forem alterados em ambos os repositórios de dados em algum momento entre sincronizações. Com a capacidade de detectar conflitos, um aplicativo pode certificar-se de que as alterações não sejam perdidas.  
  
## <a name="how-change-tracking-works"></a>Como o controle de alterações funciona  
 Para configurar o controle de alterações, você pode usar instruções DDL ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Habilitar e desabilitar o controle de alterações &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md). Para controlar alterações, o controle de alterações deve ser habilitado no banco de dados e, então, nas tabelas que você deseja controlar no banco de dados. A definição da tabela não precisa sofrer nenhuma alteração, e nenhum gatilho é criado.  
  
 Após a configuração do controle de alterações para uma tabela, qualquer instrução DML que afete as linhas da tabela fará com que as informações do controle de alterações de cada linha modificada sejam registradas. Para consultar as linhas que foram alteradas e obter informações sobre as alterações, você pode usar as [funções de controle de alterações](/sql/relational-databases/system-functions/change-tracking-functions-transact-sql).  
  
 Os valores da coluna de chave primária são as únicas informações da tabela controlada que são registradas com as informações sobre as alterações. Esses valores identificam as linhas que foram alteradas. Para obter os últimos dados sobre essas linhas, um aplicativo pode usar os valores da coluna de chave primária para unir a tabela de origem à tabela controlada.  
  
 As informações sobre a alteração feita em cada linha também podem ser obtidas usando o controle de alterações. Por exemplo, o tipo de operação DML que causou a alteração (inserção, atualização ou exclusão) ou as colunas que foram alteradas como parte de uma operação de atualização.  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar e desabilitar Controle de Alterações &#40;SQL Server&#41;](../track-changes/enable-and-disable-change-tracking-sql-server.md)   
 [Trabalhar com Controle de Alterações &#40;SQL Server&#41;](../track-changes/work-with-change-tracking-sql-server.md)   
 [Gerenciar Controle de Alterações &#40;SQL Server&#41;](../track-changes/manage-change-tracking-sql-server.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../track-changes/track-data-changes-sql-server.md)  
  
  
