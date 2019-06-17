---
title: Propriedades do item de servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- item-specific properties [Reporting Services]
- report items [Reporting Services], properties
- items [Reporting Services], properties
ms.assetid: 21edec6d-9897-48fb-8c75-182305b1dbdb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6ed8a56892cfd70b43341ffff8349faa56094a97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62519136"
---
# <a name="report-server-item-properties"></a>Propriedades do item do servidor de relatório
  As propriedades de item são propriedades específicas de itens do banco de dados do servidor de relatório. Tais itens incluem relatórios, relatórios vinculados, pastas, recursos, modelos e fontes de dados.  
  
 Os nomes de propriedade do item a seguir estão reservados. Você não pode criar propriedades definidas pelo usuário com o mesmo nome. Você poderá ler ou modificar muitas dessas propriedades usando os métodos do serviço Web Servidor de Relatório.  
  
## <a name="item-properties"></a>Propriedades do item  
 As propriedades a seguir se aplicam a todos os itens do banco de dados do servidor de relatório.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**CreatedBy**|O nome do usuário que originalmente adicionou o item ao banco de dados do servidor de relatório.|  
|**CreationDate**|A data e a hora em que o item foi adicionado ao banco de dados do servidor de relatório.|  
|**Descrição**|A descrição do item.|  
|**Oculto**|Um valor que indica se o item está visível e disponível para usuários.|  
|**ID**|A ID de um item no banco de dados do servidor de relatório.|  
|**ModifiedBy**|O nome do usuário que modificou o item por último no banco de dados do servidor de relatório.|  
|**ModifiedDate**|A data e a hora em que o usuário modificou o item pela última vez.|  
|**Nome**|O nome de um item no banco de dados do servidor de relatório.|  
|**Caminho**|O nome do caminho completo do item. O caminho de qualquer item do banco de dados do servidor de relatório tem um comprimento máximo de caracteres de 260.|  
|**Tamanho**|O tamanho, em bytes, de um item no banco de dados do servidor de relatório.|  
|**Tipo**|O tipo de um item no banco de dados do servidor de relatório.|  
|**VirtualPath**|O caminho virtual para um item no banco de dados do servidor de relatório. O valor da propriedade <xref:ReportService2010.CatalogItem.VirtualPath%2A> é o caminho sob o qual um usuário espera ver o item. Por exemplo, um relatório chamado relatório1, que está localizado na pasta Meus Relatórios pessoal do usuário, tem um caminho virtual /Meus Relatórios. O caminho real do item é /Usuários/nome de usuário/Meus Relatórios.|  
  
## <a name="folder-properties"></a>Pasta Propriedades  
 Além das propriedades do item previamente listadas, a propriedade a seguir se aplica a pastas do banco de dados do servidor de relatório.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Reserved**|Um valor retornado pelo método <xref:ReportService2010.ReportingService2010.GetProperties%2A> para pastas reservadas pelo servidor de relatório. As pastas reservadas incluem Usuários, Meus Relatórios e /. As pastas reservadas não podem ser modificadas ou removidas.|  
  
## <a name="report-properties"></a>Propriedades de relatório  
 Além das propriedades do item previamente listadas, as propriedades a seguir se aplicam a relatórios do banco de dados do servidor de relatório.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Idioma**|O idioma usado em um relatório. O valor é um código de idioma definido na especificação RFC1766 do IETF. A primeira parte é uma designação de dois caracteres do idioma básico. A segunda parte é separada por um hífen e indica a variação ou o dialeto do idioma. Se um valor não for especificado no elemento `Style` associado ao elemento `Body` na definição de relatório, o valor padrão será o idioma do servidor de relatório.|  
|`ReportProcessingTimeout`|O tempo limite, em segundos, para um relatório individual. Se esse valor for definido, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado tiver decorrido. Os valores válidos são de `-1` até `2`,`147`,`483`,`647`. Se o valor for `-1`, o relatório não terá seu limite expirado durante o processamento. Se o valor for `null`, o valor da propriedade do sistema `ReportProcessingTimeout` é usado para o tempo de limite de processamento de relatório. O valor padrão é `null`. Para obter mais informações, consulte [Propriedades de sistema do servidor de relatório](reporting-services-properties-report-server-system-properties.md).|  
|**ExecutionDate**|A data e hora em que um instantâneo de relatório foi criado pela última vez para um relatório.|  
|**CanRunUnattended**|Um valor que indica se um relatório pode ser executado em estado autônomo em uma agenda. Se essa propriedade for definida como `true`, os valores padrão para parâmetros de relatório serão definidos e as credenciais de fonte de dados serão armazenadas com o relatório, ou a opção de recuperação de credencial será definida como `None`. Se essa propriedade for definida como `false`, não serão atendidos os pré-requisitos para a execução autônoma de um relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma do &#40;Configuration Manager do SSRS&#41;](../../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).|  
|**HasParameterDefaultValues**|Um valor que indica se o relatório tem valores padrão válidos definidos para todos os parâmetros de relatório. O valor também será `true` se um relatório não tiver parâmetros de relatório. Se essa propriedade for definida como `false`, um ou mais parâmetros de relatório não terão um valor padrão válido.|  
|**HasDataSourceCredentials**|Um valor que indica que a opção de recuperação de credencial definida para todas as fontes de dados associadas ao relatório é `None` ou `Store`. Se essa propriedade for definida como `false`, uma opção de recuperação de credencial definida para uma das fontes de dados associadas ao relatório será `Integrated` ou `Prompt`.|  
|**IsSnapshotExecution**|Um valor que indica se o relatório é um instantâneo.|  
|**HasScheduleReadyDataSources**|Um valor que indica se as fontes de dados de um relatório são configuradas para dar suporte à execução agendada. Se essa propriedade for definida como `false`, os usuários não poderão assinar o relatório.|  
  
## <a name="resource-properties"></a>Propriedades de recurso  
 Além das propriedades do item previamente listadas, a propriedade a seguir se aplica a recursos do banco de dados do servidor de relatório.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**MimeType**|O tipo MIME de um recurso no banco de dados do servidor de relatório.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
