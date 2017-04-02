---
title: "Considera&#231;&#245;es administrativas sobre Oracle Publishers | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação Oracle [replicação do SQL Server], considerações administrativas"
  - "administrando a replicação, publicação Oracle"
ms.assetid: cfd81fb5-419b-4a1b-97c4-be7c9d4ee289
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Considera&#231;&#245;es administrativas sobre Oracle Publishers
  Após configurar um Editor Oracle e ativar os mecanismos de rastreamento de alterações de replicação, os administradores do sistema de banco de dados Oracle ainda podem usar os utilitários de banco de dados padrão Oracle e realizar tarefas típicas de administração de sistemas. Porém, você deve estar ciente quanto aos efeitos que a execução de certas tarefas administrativas pode ter nos dados publicados.  
  
 Com exceção de descartar ou modificar uma coluna publicada para replicação e descartar ou modificar qualquer objeto de replicação, essas considerações não se aplicam à publicação de instantâneos.  
  
## Importando e carregando dados  
 Gatilhos são usados para rastrear alterações em publicações transacionais no Oracle. As alterações em tabelas publicadas podem ser replicadas para os Assinantes apenas se os gatilhos de replicação forem acionados quando ocorrer uma atualização, uma inserção ou uma exclusão. Os utilitários Oracle Import e SQL*Loader, da Oracle, têm opções que afetam o acionamento dos gatilhos quando linhas são inseridas em tabelas replicadas com esses utilitários.  
  
### Oracle Import  
 Com o Oracle Import, você pode definir a opção **Ignorar** para 'y' ou ' n' (o padrão é ' n '). Se **Ignorar** é definido como ' n ', a tabela será descartada e recriada durante a importação. Isso remove os gatilhos de replicação e desabilita a replicação. Se **Ignorar** é definido como 's'importação tentará carregar as linhas na tabela existente, que aciona os gatilhos de replicação. Portanto, certifique-se de **Ignorar** é definido como 'y' ao importar para uma tabela replicada com a ferramenta de importação.  
  
### SQL*Loader  
 Com o SQL\*Loader, você pode definir a opção **direto** como 'true' ou 'false' (o padrão é 'false'). Se **direto** é definido como 'false', serão inseridas linhas usando instruções convencionais INSERT que acionam gatilhos de replicação. Se **direto** é definido como 'true', a carga será otimizada e não os gatilhos são acionados. Portanto, certifique-se de **direto** é definido como 'false' durante o carregamento em uma tabela replicada com o SQL * ferramenta carregador.  
  
## Fazendo alterações em objetos publicados  
 As seguintes ações não requerem nenhuma consideração especial:  
  
-   Reconstruir índices em tabelas publicadas.  
  
-   Adicionar gatilhos de usuário a uma tabela publicada.  
  
 A ação a seguir exige que você interrompa toda a atividade nas tabelas publicadas:  
  
-   Mover uma tabela publicada.  
  
 As ações a seguir exigem que você descarte a publicação, execute a operação e então recrie a publicação:  
  
-   Truncar uma tabela publicada.  
  
-   Renomear uma tabela publicada.  
  
-   Adicionar uma coluna a uma tabela publicada.  
  
-   Descartar ou modificar uma coluna que é publicada para replicação.  
  
-   Executar operações não registradas.  
  
## Descartar ou modificar objetos de replicação  
 Você deve descartar e reconfigurar o Publicador se descartar ou modificar qualquer tabela de rastreamento de nível, sequência ou procedimento armazenado do Editor. Para obter uma lista parcial destes objetos, consulte [objetos criados no editor Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md).  
  
 Para obter informações sobre como descartar e reconfigurar o publicador, consulte a seção "São feitas alterações que exigem reconfiguração do publicador" no tópico [problemas de editores Oracle](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
## Consulte também  
 [Configurar um publicador Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Considerações de design e limitações para Publicadores Oracle](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)   
 [Visão geral da Publicação Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  