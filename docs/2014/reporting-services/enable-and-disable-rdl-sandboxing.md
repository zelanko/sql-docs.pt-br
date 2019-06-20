---
title: Habilitar e desabilitar o RDL Sandboxing | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d5619e9f-ec5b-4376-9b34-1f74de6fade7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebc5ee51dd32cb999f0e6551bb87c36eda8865c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109232"
---
# <a name="enable-and-disable-rdl-sandboxing"></a>Habilitar e desabilitar o RDL Sandboxing
  O recurso RDL Sandboxing (Linguagem RDL) permite que você detecte e restrinja o uso de tipos específicos de recurso por locatários individuais em um ambiente de vários locatários que utilizam um único web farm de servidores de relatório. Um exemplo disso é um cenário de serviços de hospedagem onde você poderia manter um único web farm de servidores de relatório que são usados por vários locatários e talvez empresas diferentes. Como administrador de servidor de relatório, você pode permitir que esse recurso ajude a obter os objetivos seguintes:  
  
-   Restringir tamanhos de recursos externos. Recursos externos incluem imagens, arquivos .xslt e dados de mapa.  
  
-   Na hora da publicação do relatório, tipos de limite e membros que são usados em texto de expressão.  
  
-   Na hora do processamento do relatório, limite o comprimento do texto e o tamanho do valor de retorno para expressões.  
  
 Quando o RDL Sandboxing está habilitado, os seguintes recursos são desabilitados:  
  
-   Código personalizado no elemento **\<Code>** de uma definição de relatório.  
  
-   Modo de compatibilidade com versões anteriores do RDL para itens de relatório personalizados do [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] .  
  
-   Parâmetros nomeados em expressões.  
  
 Este tópico descreve cada elemento de <`RDLSandboxing`> elemento no arquivo rsreportserver. config. Para obter mais informações sobre como modificar esse arquivo, veja [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Um log de rastreamento de servidor registra atividade relacionada ao recurso RDL Sandboxing. Para obter mais informações sobre logs de rastreamento, consulte [Log de rastreamento do serviço Servidor de Relatório](report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Configuração de exemplo  
 O exemplo a seguir mostra as configurações e valores de exemplo para o <`RDLSandboxing`> elemento no arquivo rsreportserver. config.  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace="System.Drawing" AllowNew="True">Bitmap</Allow>  
      <Allow Namespace="TypeConverters.Custom" AllowNew="True">*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```  
  
## <a name="configuration-settings"></a>Definições de configuração  
 A tabela a seguir fornece informações sobre definições de configuração. As configurações são apresentadas na ordem em que aparecem no arquivo de configuração.  
  
|Configuração|Descrição|  
|-------------|-----------------|  
|**MaxExpressionLength**|Número máximo de caracteres permitido em expressões RDL.<br /><br /> Padrão: 1.000|  
|**MaxResourceSize**|Número máximo de KB permitido em um recurso externo.<br /><br /> Padrão: 100|  
|**MaxStringResultLength**|Número máximo de caracteres permitido em um valor de retorno para uma expressão RDL.<br /><br /> Padrão: 1.000|  
|**MaxArrayResultLength**|Número máximo de itens permitido em um valor de resposta de matrizes para uma expressão RDL.<br /><br /> Padrão: 100|  
|**Types**|A lista de membros para permitir dentro de expressões RDL.|  
|**Allow**|Um tipo ou conjunto de tipos para permitir em expressões RDL.|  
|**Namespace**|Atributo para **Allow** que é o namespace que contém um ou mais tipos que se aplicam a Valor. Esta propriedade não diferencia maiúsculas e minúsculas.|  
|`AllowNew`|Atributo booliano para **Allow** que controla se novas instâncias do tipo têm permissão para serem criadas em expressões RDL ou em um elemento RDL **\<Class>** .<br /><br /> Observação: Quando `RDLSandboxing` estiver habilitado, novas matrizes não podem ser criadas em expressões RDL, independentemente da configuração de `AllowNew`.|  
|**Value**|Valor para **Allow** que é o nome do tipo para permitir em expressões RDL. O valor **\*** indica que todos os tipos no namespace são permitidos. Esta propriedade não diferencia maiúsculas e minúsculas.|  
|**Membros**|Para a lista de tipos incluídos no elemento **\<Types>** , a lista de nomes de membros que não são permitidos em expressões RDL.|  
|**Deny**|O nome de um membro que não é permitido em expressões RDL. Esta propriedade não diferencia maiúsculas e minúsculas.<br /><br /> Observação: Quando **Deny** é especificado para um membro, nenhum membro com esse nome para todos os tipos é permitido.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>Trabalhando com expressões quando o RDL Sandboxing está habilitado  
 Você pode modificar o recurso RDL Sandboxing para gerenciar os recursos que são usados por uma expressão das seguintes maneiras:  
  
-   Restrinja o número de caracteres que são usados para uma expressão.  
  
-   Restrinja o tamanho do resultado retornado por uma expressão.  
  
-   Permita uma lista específica de tipos que podem ser usados em uma expressão.  
  
-   Restrinja a lista de membros por nome para a lista de tipos permitidos que podem ser usados em uma expressão.  
  
-   O recurso RDL Sandboxing permite criar uma lista de tipos aprovados e uma lista de membros negados. A lista de tipos aprovados é chamada de lista de permissões. A lista de membros negados é chamada de lista de contatos bloqueados.  
  
> [!NOTE]  
>  Na definição de relatório, um computador não pode saber o tipo de todas as instâncias de uma referência de expressão. Quando você acrescentar um membro à lista de contatos bloqueados, estará negando todos os membros daquele nome em todos os tipos na lista de permissões.  
  
 Resultados de expressão RDL são verificados em tempo de execução. Expressões RDL são verificadas na definição de relatório quando o relatório é publicado. Monitore o log de rastreamento de servidor de relatório em busca de violações. Para obter mais informações, consulte [Report Server Service Trace Log](report-server/report-server-service-trace-log.md).  
  
### <a name="working-with-types"></a>Trabalhando com tipos  
 Quando você acrescentar um tipo à lista de permissões, estará controlando os seguintes pontos de entrada para acessar expressões RDL:  
  
-   Membros estáticos de um tipo.  
  
-   O [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] `New` método.  
  
-   O elemento **\<Classes>** na definição de relatório.  
  
-   Membros que você acrescentou à lista de contatos bloqueados para um tipo na lista de permissões.  
  
 A lista de permissões não controla os seguintes pontos de entrada:  
  
-   Conjuntos de dados de relatório. Campos em conjuntos de dados de relatório que são retornados de consultas que possam conter algum tipo RDL válido.  
  
-   Parâmetros de relatório. Os valores de parâmetros fornecidos pelo usuário podem conter algum tipo RDL válido.  
  
-   Membros de um tipo habilitado que não estão na lista de contatos bloqueados. Por padrão, todos os membros de todos os tipos são habilitados na lista de permissões. Quando você acrescentar um nome de membro à lista de contatos bloqueados, estará negando todos os membros com aquele nome em todos os tipos que estiverem na lista de permissões.  
  
 Para habilitar um membro de um tipo mas negar um membro com o mesmo nome para um tipo diferente, você deve fazer o seguinte:  
  
-   Adicione um elemento **\<Deny>** ao nome do membro.  
  
-   Crie um membro de proxy com um nome diferente em uma classe em um assembly personalizado para o membro que você deseja habilitar.  
  
-   Acrescente aquela nova classe à lista de permissões.  
  
 Para acrescentar funções de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework à lista de permissões, acrescente os tipos correspondentes do namespace Microsoft.VisualBasic à lista de permissões.  
  
 Para acrescentar palavras-chave de tipo do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework à lista de permissões, acrescente o tipo CLR correspondente à lista de permissões. Por exemplo, para usar o [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] palavra-chave do .NET Framework `Integer`, adicione o seguinte fragmento XML para o  **\<RDLSandboxing >** elemento:  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 Para acrescentar um tipo genérico ou que permite valor nulo do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework à lista de permissões, você deve fazer o seguinte:  
  
-   Crie um tipo de proxy para o tipo genérico ou anulável do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework.  
  
-   Acrescente um tipo de proxy à lista de permissões.  
  
 Acrescentar um tipo de um assembly personalizado à lista de permissões não concede implicitamente permissão de execução no assembly. Você deve modificar especificamente o arquivo de segurança de acesso a código e fornecer permissão de execução ao assembly. Para obter mais informações, veja [Segurança de acesso do código no Reporting Services](extensions/secure-development/code-access-security-in-reporting-services.md).  
  
#### <a name="maintaining-the-deny-list-of-members"></a>Manter o \<Deny > lista de membros  
 Quando você acrescentar um tipo à lista de permissões, use a lista a seguir para determinar quando você deverá atualizar a lista de membros bloqueados.  
  
-   Quando você atualiza um assembly personalizado com uma versão que introduz novos tipos.  
  
-   Quando você acrescenta os membros aos tipos na lista de permissões.  
  
-   Quando você atualiza o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] no servidor de relatório.  
  
-   Quando você atualiza o servidor de relatório para uma versão mais recente do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Quando você atualiza um servidor de relatório para tratar um esquema de RDL posterior, porque novos membros podem ter sido adicionados a tipos RDL.  
  
### <a name="working-with-operators-and-new"></a>Trabalhando com operadores e novo  
 Por padrão, os operadores de linguagem do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework, com exceção de `New`, são sempre permitidos. O `New` operador é controlado pelo `AllowNew` atributo as  **\<permitir >** elemento. Outros operadores de linguagem, como o operador de acessador de coleção padrão `!` e [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework macros de conversão, como `CInt`, são sempre permitidos.  
  
 Acrescentar operadores a uma lista de contatos bloqueados, incluindo operadores personalizados, não tem suporte. Para excluir operadores para um tipo, você deve fazer o seguinte:  
  
-   Crie um tipo de proxy que não implementa os operadores que você deseja excluir.  
  
-   Acrescente um tipo de proxy à lista de permissões.  
  
 Para criar uma nova matriz em uma expressão RDL, crie a matriz em um método em uma classe que você define e acrescente essa classe à lista de permissões.  
  
 Para criar uma nova matriz em uma expressão RDL, você deve fazer o seguinte:  
  
-   Defina uma nova classe e crie a matriz em um método nessa classe.  
  
-   Acrescente a classe à lista de permissões.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de configuração RSReportServer](report-server/rsreportserver-config-configuration-file.md)   
 [Log de rastreamento do serviço Servidor de Relatório](report-server/report-server-service-trace-log.md)  
  
  
