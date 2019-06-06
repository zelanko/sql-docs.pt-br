---
title: Problemas de Design de segurança ADO | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1b098733eccd03db7bafff084fdc2416ddff5845
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701754"
---
# <a name="ado-security-design-features"></a>Recursos de Design de segurança do ADO
As seções a seguir descrevem os recursos de design de segurança no ActiveX Data Objects (ADO) 2.8 e posterior. Essas alterações foram feitas no ADO 2.8 para melhorar a segurança. ADO 6.0, que está incluído no Windows DAC 6.0 no Windows Vista, é funcionalmente equivalente ao ADO 2.8, que foi incluído no MDAC 2.8 no Windows XP e Windows Server 2003. Este tópico fornece informações sobre como proteger melhor seus aplicativos no ADO 2.8 ou posterior.

> [!IMPORTANT]
>  Se você estiver atualizando seu aplicativo de uma versão anterior do ADO, é recomendável que você teste seu aplicativo atualizado em um computador não seja de produção antes de implantá-lo aos clientes. Dessa forma, você pode garantir que estão cientes dos problemas de compatibilidade antes de implantar seu aplicativo atualizado.

## <a name="internet-explorer-file-access-scenarios"></a>Cenários de acesso de arquivo do Internet Explorer
 O seguinte efeito de recursos como o ADO 2.8 e posterior funciona quando ele é usado no script páginas da Web no Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Caixa de mensagem de aviso de segurança aprimorada e revisado agora é usada para alertar os usuários
 Para ADO 2.7 e anterior, a seguinte mensagem de aviso será exibida quando uma página da Web com script tenta executar código em ADO em um provedor de não confiável:

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Para ADO 2.8 e posterior, a mensagem anterior não aparece mais. Em vez disso, a seguinte mensagem será exibida neste contexto:

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite que o usuário tome uma decisão informada, sabendo as consequências de qualquer uma dessas opções:

-   Se o site de confiança do usuário, clicando em Okey permitirá que todo o código safe de disco (todos os métodos do ADO e propriedades com as exceções das APIs do disco acessível descritas mais adiante neste tópico) para executar e executar na janela do navegador.

-   Se o usuário não confia no site, clicar em Cancelar bloqueia o código do ADO para acesso a dados de execução e a operação em sua totalidade.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Código acessível ao disco agora limitado aos sites confiáveis
 Foram feitas alterações adicionais no ADO 2.8 que restrinjam especificamente a capacidade de um conjunto limitado de APIs, o que pode expor o potencial para ler ou gravar em arquivos no computador local. Aqui estão os métodos da API que foram mais restrito para fornecer segurança ao executar o Internet Explorer:

-   Para o ADO **Stream** do objeto, se o [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) ou [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) métodos são usados.

-   Para o ADO **conjunto de registros** do objeto, se qualquer um da [salvar](../../ado/reference/ado-api/save-method.md) método ou o [abrir](../../ado/reference/ado-api/open-method-ado-recordset.md) método, por exemplo, quando qualquer um do **adCmdFile** opção for definida ou o [provedor Microsoft OLE DB persistência (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) é usado.

 Para esses conjuntos limitados de funções potencialmente acessível de disco, ocorrerá o seguinte comportamento para ADO 2.8 e posterior, se qualquer código que usa esses métodos é executado no Internet Explorer:

-   Se o site que forneceu o código foi adicionado anteriormente à lista de zona Sites confiáveis, o código é executado no navegador e o acesso é concedido a arquivos locais.

-   Se o site não aparecer na lista de zona de Sites confiáveis, o código será bloqueado e é negado acesso a arquivos locais.

    > [!NOTE]
    >  No ADO 2.8 e posterior, o usuário não é alertado ou orientado a adicionar sites à lista de zona Sites confiáveis. Portanto, o gerenciamento da lista de Sites confiáveis é a responsabilidade de quem estiver implantando ou dar suporte a aplicativos baseados no site da Web que exigem acesso ao sistema de arquivos local.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Acesso bloqueado para a propriedade ActiveCommand em objetos de conjunto de registros
 Quando em execução no Internet Explorer, o ADO 2.8 agora bloqueia o acesso a [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) propriedade para um ativo **conjunto de registros** do objeto e retornará um erro. O erro ocorre, independentemente se a página é proveniente de um site da Web registrado na lista de Sites confiáveis.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Alterações na manipulação de provedores OLE DB e a segurança integrada
 Ao revisar ADO 2.7 e versões anteriores para possíveis problemas de segurança e preocupações, o cenário a seguir foi descoberto:

 Em alguns casos, os provedores OLE DB que dão suporte a segurança integrada [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) propriedade poderia potencialmente permitir com script páginas da Web para reutilizar o objeto de Conexão do ADO para conectar-se inadvertidamente a outros servidores usando as credenciais de logon atual dos usuários. Para evitar isso, o ADO 2.8 e posterior lidar com provedores de OLE DB, dependendo de como que escolheram para fornecer ou fornecer, para a segurança integrada.

 Para páginas da Web que são carregadas de sites listados na lista de zona de Sites confiáveis, a tabela a seguir fornece uma análise de como o ADO 2.8 e posterior gerencia conexões ADO em cada caso.

|Configurações do IE para autenticação de usuário de logon|Provedor oferece suporte a "Segurança integrada" e UID e PWD estão especificados (SQLOLEDB)|Provedor não dá suporte a "Segurança integrada" (JOLT, MSDASQL, MSPersist)|Provedor oferece suporte a "Segurança integrada" e é definida como SSPI (nenhum UID/PWD forem especificados)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Logon automático com o nome de usuário atual e a senha|Permitir conexão|Permitir conexão|Permitir conexão|
|Solicitar nome de usuário e senha|Permitir conexão|Falha de conexão|Falha de conexão|
|Logon automático somente na zona da Intranet|Permitir conexão|Solicitar ao usuário com o aviso de segurança|Solicitar ao usuário com o aviso de segurança|
|Logon anônimo|Permitir conexão|Falha de conexão|Falha de conexão|

 No caso em que um aviso de segurança agora é exibido, a caixa de mensagem informa aos usuários:

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite que o usuário tome uma decisão mais informada e proceda conforme necessário.

> [!NOTE]
>  Para sites não confiáveis (ou seja, sites não listados na lista de zona de Sites confiáveis), se o provedor também não é confiável (como discutido no início desta seção), o usuário verá dois avisos de segurança em uma linha, um aviso sobre o provedor não seguro e um segundo aviso o tentativa de usar sua identidade. Se o usuário clica Okey para o primeiro aviso, as configurações do Internet Explorer e o código de comportamento de resposta descritos na tabela anterior são executadas.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controlar se o texto da senha é retornado em cadeias de caracteres de conexão ADO
 Quando você tentar obter o valor da [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade em ADO **Conexão** do objeto, os seguintes eventos ocorrem:

1.  Se a conexão estiver aberta, uma chamada de inicialização é feita para o provedor OLE DB subjacente para obter a cadeia de conexão.

2.  Dependendo da configuração no provedor do OLE DB do [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) propriedade, as senhas são incluídas junto com outras informações de cadeia de caracteres de conexão que são retornadas.

 Por exemplo, se a propriedade dinâmica de Conexão ADO **Persist Security Info** é definido como **verdadeiro**, informações de senha estão incluídas na cadeia de conexão retornada. Caso contrário, se o provedor subjacente tiver definido a propriedade como **falsos** (por exemplo, com o provedor SQLOLEDB), as informações de senha for omitidas na cadeia de conexão retornado.

 Se você estiver usando produtos de terceiros (ou seja, não são da Microsoft) provedores OLE DB com o código do aplicativo ADO, você pode verificar como o **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** propriedade é implementada para determinar se a inclusão de informações de senha com cadeias de caracteres de conexão ADO são permitidas.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Procurando dispositivos diferentes de arquivos ao carregar e salvar conjuntos de registros ou fluxos
 Para ADO 2.7 e anterior, arquivo operações de entrada/saída, como [aberto](../../ado/reference/ado-api/open-method-ado-recordset.md) e [salvar](../../ado/reference/ado-api/save-method.md) que foram usados para ler e gravar dados com base em arquivo em alguns casos permitiria um URL ou nome de arquivo a ser usado que especificou um disco não- com base em tipo de arquivo. Por exemplo, LPT1, COM2, PRN. TXT, AUX pode ser usado como um alias de entrada/saída entre as impressoras e os dispositivos auxiliares no sistema usando determinados

 Para ADO 2.8 e posterior, essa funcionalidade foi atualizada. Para abrir e salvar **conjunto de registros** e **Stream** objetos, ADO agora executa uma verificação de tipo de arquivo para garantir que o dispositivo de entrada ou de saída especificado em um URL ou nome de arquivo é um arquivo real.

> [!NOTE]
>  Verificação de tipo de arquivo conforme descrito nesta seção se aplica somente para o Windows 2000 e posterior. Não é aplicável a situações em que o ADO 2.8 ou posterior está em execução em versões anteriores do Windows, como o Windows 98.
