---
title: Configurar propriedades de um coletor de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollectionprop.general.f1
- sql13.swb.dc.datacollectionprop.advanced.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 67df1557cf4035f4e7bfca1eaa23d9bb0505c8e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62945509"
---
# <a name="configure-properties-of-a-data-collector"></a>Configurar propriedades de um coletor de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar coleta de dados](../../relational-databases/data-collection/manage-data-collection.md)   
 [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
