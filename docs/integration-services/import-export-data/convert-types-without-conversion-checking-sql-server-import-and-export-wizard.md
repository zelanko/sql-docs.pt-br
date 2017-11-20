---
title: "Converter tipos sem verificação (Assistente de importação-exportação do SQL Server) de conversão | Microsoft Docs"
ms.custom: 
ms.date: 01/11/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4b3bfd3d61282ba7a4d7363ef02b05c5c23ac20
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>Converter tipos sem verificação de conversão (Assistente de Importação e Exportação do SQL Server)
  Depois de selecionar as tabelas existentes e exibições para copiar ou examinar a consulta que você forneceu, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode mostrar **Converter tipos sem verificar a conversão**. O assistente mostra essa página quando não é possível localizar um ou mais dos arquivos de mapeamento e de conversão de tipo de dados necessários para mapear os tipos de dados entre a origem e o destino. A página inclui informações que ajudam você a compreender o que está faltando.
  
 Clique em **Avançar** para continuar sem saber se as conversões de tipo de dados serão bem-sucedidas. Caso contrário, clique em **Voltar** para alterar suas seleções ou clique em **Cancelar** para sair do assistente.

## <a name="screen-shot-of-the-convert-types-page"></a>Captura de tela da página Converter Tipos  
  
A captura de tela a seguir mostra um exemplo da página **Converter Tipos sem Verificar a Conversão** do Assistente.

![Converter tipos](../../integration-services/import-export-data/media/convert-types.png)

O problema aqui é que o assistente não pode encontrar um arquivo de mapeamento que mapeia tipos de dados para o destino selecionado.

As informações desta página não incluem o nome do arquivo de mapeamento ausente. Como o assistente não sabe se um arquivo existe para o provedor de dados especificado, ele não pode fornecer um nome para o arquivo ausente.

## <a name="whats-next"></a>O que vem a seguir?  
 Após clicar em **Avançar** para continuar sem saber se as conversões de tipo de dados serão bem-sucedidas, a próxima página será **Salvar e Executar o Pacote**. Nesta página, especifique se deseja executar a operação de cópia imediatamente. Dependendo da sua configuração, você também poderá salvar o pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

## <a name="see-also"></a>Consulte também
[Mapeamento de Tipo de Dados no Assistente para Importação e Exportação do SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)

