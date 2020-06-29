---
title: Definir valores de parâmetro depois que o projeto for implantado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 39572594e429b61de0641c6e6929e84105138f1f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421613"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>Definir valores de parâmetros depois que o projeto foi implantado
  O Assistente de Implantação permite definir valores de parâmetros padrão de servidor ao implantar seu projeto no catálogo. Depois que seu projeto estiver no catálogo, você pode usar o Pesquisador de Objetos do SQL Server Management Studio (SSMS) ou o Transact-SQL para definir valores padrão de servidor.  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>Para definir padrões de servidor com Pesquisador de Objetos do SSMS:  
  
1.  Selecione e clique com o botão direito do mouse no projeto sob o nó **Integration Services**.  
  
2.  Clique em **Propriedades** para abrir janela da caixa de diálogo **Propriedades do Projeto**.  
  
3.  Abra a página de parâmetros com um clique em **Parâmetros** sob **Selecionar uma página**.  
  
4.  Selecione o parâmetro desejado na lista **Parâmetros**. Observação: a coluna **Contêiner** ajuda a distinguir os parâmetros de projeto dos parâmetros de pacote.  
  
5.  Na coluna **Valor**, especifique o valor do parâmetro padrão de servidor desejado.  
  
 Para definir padrões de servidor com Transact-SQL, use o procedimento armazenado [catalog.set_object_parameter_value &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database). Para exibir os padrões atuais de servidor, consulte a exibição [catalog.object_parameters &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database). Para apagar um valor padrão de servidor, use o procedimento armazenado [catalog.clear_object_parameter_value &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database).  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services parâmetros&#41; &#40;SSIS](integration-services-ssis-package-and-project-parameters.md)  
  
  
