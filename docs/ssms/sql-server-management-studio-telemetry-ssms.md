---
title: SQL Server Management Studio – Telemetria (SSMS) | Microsoft Docs
ms.custom: ''
ms.date: 02/20/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce4abde855b5fe6a65c3038e93eb8609f9736dc1
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240384"
---
# <a name="local-audit-for-ssms-usage-and-diagnostic-data-collection"></a>Auditoria local para coleta de dados de diagnóstico e uso do SSMS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

O SSMS (SQL Server Management Studio) contém recursos habilitados para Internet que podem coletar e enviar os dados anônimos de diagnóstico e uso de recursos à Microsoft. O SSMS pode coletar informações padrão do computador e informações de uso e desempenho que podem ser transmitidas à Microsoft e analisadas com a finalidade de aprimorar a qualidade, a segurança e a confiabilidade do SSMS. Não coletamos dados como o seu nome, endereço ou outras informações de contato. Para obter detalhes, confira a [Declaração de privacidade da Microsoft](https://privacy.microsoft.com/privacystatement) e [Suplemento de Privacidade do SQL Server](https://go.microsoft.com/fwlink/?LinkID=868444).

## <a name="audit-feature-usage-data"></a>Dados de uso do recurso de auditoria

Para ver os dados de uso do recurso que são coletados pelo SSMS, faça o seguinte:
1.  Inicie o SSMS.
2.  Clique em **Exibir**, depois clique em **Saída** no menu principal para mostrar a janela **Saída**. 
3.  Quando a janela **Saída** estiver visível, escolha **Telemetria** no menu **Mostrar saída de:**.

Ao usar o SSMS para interagir com bancos de dados, a janela **Saída** mostra os dados coletados.

## <a name="enable-or-disable-usage-feedback-collection-in-ssms"></a>Habilitar ou desabilitar a coleta de comentários sobre o uso no SSMS

Para aceitar ou recusar a coleta de dados de uso para SSMS:

- Para o SQL Server Management Studio 17:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\14.0`

  Nome da RegEntry= `UserFeedbackOptIn`

  Tipo de entrada `DWORD`: `0` é recusar; `1` é aceitar

  Além disso, o SSMS 17.x baseia-se no shell do Visual Studio 2015, e a instalação do Visual Studio permite comentários do cliente por padrão.  

  Para configurar o Visual Studio para desabilitar os comentários do cliente em computadores individuais, altere o valor da seguinte subchave do Registro para a cadeia de caracteres `0`: `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn`

  Por exemplo, altere a subchave para o seguinte:  
  `HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\VisualStudio\SQM OptIn `=` 0`

  A Política de Grupo baseada em registros nessas sub-chaves de registro é cumprida pela coleta de dados de diagnóstico e uso do SQL Server 2017.

- Para o SQL Server Management Studio 18:

  `Subkey = HKEY_CURRENT_USER\Software\Microsoft\SQL Server Management Studio\18.0_IsoShell`

  Nome da RegEntry= `UserFeedbackOptIn`

  Tipo de entrada `DWORD`: `0` é recusar; `1` é aceitar

## <a name="see-also"></a>Confira também

- [Configurar a coleta de dados de diagnóstico e uso do SQL Server](../sql-server/usage-and-diagnostic-data-configuration-for-sql-server.md)
- [Auditoria local para coleta de dados de diagnóstico e uso do SQL Server](http://msdn.microsoft.com/library/mt743085.aspx)
