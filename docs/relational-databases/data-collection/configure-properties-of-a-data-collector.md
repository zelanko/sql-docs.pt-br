---
title: Configurar propriedades de um coletor de dados | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dc.datacollectionprop.general.f1
- sql13.swb.dc.datacollectionprop.advanced.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2a0aad98c302e55b3edc76b01fc0c5eae4e249ac
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="configure-properties-of-a-data-collector"></a>Configurar propriedades de um coletor de dados
  Este tópico discute como você pode configurar as propriedades de um coletor de dados.  
  
## <a name="data-collection-properties-general-tab"></a>Propriedades de Coleta de Dados (guia Geral)  
 Use esta página para definir configurações para o data warehouse de gerenciamento e especifique em que lugar os dados coletados devem ser armazenados antes de serem carregados no data warehouse.  
  
 **Habilitar Coleta de Dados**  
 Selecione para habilitar a coleta de dados. Essa opção tem o mesmo efeito da execução do procedimento armazenado sp_syscollector_enable_collector. Desmarcar essa caixa de seleção desabilita a coleta de dados e tem o mesmo efeito da execução do procedimento armazenado sp_syscollector_disable_collector.  
  
 **Servidor**  
 Exibe o nome do servidor que hospedará o data warehouse de gerenciamento  
  
 **Nome do banco de dados**  
 Exibe o nome do banco de dados relacional que é usado para o data warehouse de gerenciamento.  
  
 **Testar Conexão**  
 Teste a conexão ao **Servidor** especificado usando as informações fornecidas quando a coleta de dados foi configurada.  
  
 **Diretório de cache**  
 Especifica o diretório em que os dados coletados são armazenados no sistema que coleta os dados antes de eles serem carregados no data warehouse de gerenciamento. Se o **Diretório de cache** não for especificado, o coletor de dados tentará localizar o %TEMP% e as variáveis de ambiente %TMP% e usará um desses locais como local padrão para armazenamento temporário. Se essas variáveis de ambiente não forem configuradas, ocorrerá um e você será solicitado a criar um diretório de cache.  
  
## <a name="data-collection-properties-advanced-tab"></a>Propriedades de Coleta de Dados (guia Avançado)  
 Use esta página para configurar os parâmetros de tentativa da conexão ao data warehouse de gerenciamento.  
  
 **Número de tentativas se o carregamento falhar**  
 Especifica o número de novas tentativas de carregamento no data warehouse de gerenciamento se o carregamento falhar. O padrão é 1.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciar coleta de dados](../../relational-databases/data-collection/manage-data-collection.md)   
 [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
