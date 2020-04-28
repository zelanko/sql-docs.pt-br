---
title: Problemas de design de segurança do ADO | Microsoft Docs
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
ms.openlocfilehash: f638f6e48dccccd91849f02c65331d9212f9bbb7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67927034"
---
# <a name="ado-security-design-features"></a>Recursos de design de segurança do ADO
As seções a seguir descrevem os recursos de design de segurança no ActiveX Data Objects (ADO) 2,8 e posterior. Essas alterações foram feitas no ADO 2,8 para melhorar a segurança. O ADO 6,0, que está incluído no DAC 6,0 do Windows no Windows Vista, é funcionalmente equivalente ao ADO 2,8, que foi incluído no MDAC 2,8 no Windows XP e no Windows Server 2003. Este tópico fornece informações sobre como proteger melhor seus aplicativos no ADO 2,8 ou posterior.

> [!IMPORTANT]
>  Se você estiver atualizando seu aplicativo de uma versão anterior do ADO, é recomendável testar seu aplicativo atualizado em um computador que não seja de produção antes de implantá-lo para os clientes. Dessa forma, você pode garantir que está ciente de quaisquer problemas de compatibilidade antes de implantar seu aplicativo atualizado.

## <a name="internet-explorer-file-access-scenarios"></a>Cenários de acesso a arquivos do Internet Explorer
 Os recursos a seguir afetam o modo como o ADO 2,8 e posterior funciona quando é usado em páginas da Web com script no Internet Explorer.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>Caixa de mensagem de aviso de segurança revisada e aprimorada agora usada para alertar os usuários
 Para o ADO 2,7 e anterior, a seguinte mensagem de aviso é exibida quando uma página da Web com script tenta executar o código ADO de um provedor não confiável:

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 Para o ADO 2,8 e posterior, a mensagem anterior não é mais exibida. Em vez disso, a seguinte mensagem aparece neste contexto:

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite que o usuário tome uma decisão informada, sabendo as consequências para qualquer uma das duas opções:

-   Se o usuário confiar no site, clicar em OK permitirá que todo o código seja protegido por disco (todos os métodos e propriedades do ADO com as exceções das APIs acessíveis ao disco descritas posteriormente neste tópico) para executar e executar na janela do navegador.

-   Se o usuário não confiar no site, clicar em cancelar bloqueará o código ADO para que o acesso a dados seja executado e em execução em sua totalidade.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>Código acessível por disco limitado agora para sites confiáveis
 Foram feitas alterações de design adicionais no ADO 2,8 que restringem especificamente a capacidade de um conjunto limitado de APIs, o que pode expor o potencial de leitura ou gravação em arquivos no computador local. Aqui estão os métodos de API que foram ainda mais restritos quanto à segurança ao executar o Internet Explorer:

-   Para o objeto de **fluxo** ADO, se os métodos [loaddefile](../../ado/reference/ado-api/loadfromfile-method-ado.md) ou [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) forem usados.

-   Para o objeto **RECORDSET** ADO, se o método [Save](../../ado/reference/ado-api/save-method.md) ou o método [Open](../../ado/reference/ado-api/open-method-ado-recordset.md) , como quando a opção **AdCmdFile** está definida ou o [Microsoft OLE DB Persistence Provider (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) é usado.

 Para esses conjuntos limitados de funções potencialmente acessíveis ao disco, o seguinte comportamento ocorre para o ADO 2,8 e posterior, se qualquer código que usa esses métodos for executado no Internet Explorer:

-   Se o site que forneceu o código foi adicionado anteriormente à lista de zona de sites confiáveis, o código é executado no navegador e o acesso é concedido a arquivos locais.

-   Se o site não aparecer na lista de zona de sites confiáveis, o código será bloqueado e o acesso aos arquivos locais será negado.

    > [!NOTE]
    >  No ADO 2,8 e posterior, o usuário não é alertado ou aconselhado a adicionar sites à lista de zonas de sites confiáveis. Portanto, o gerenciamento da lista de sites confiáveis é responsabilidade dos que estão implantando ou oferecendo suporte a aplicativos baseados em site que exigem acesso ao sistema de arquivos local.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>Acesso bloqueado à propriedade ActiveCommand em objetos Recordset
 Ao executar no Internet Explorer, o ADO 2,8 agora bloqueia o acesso à propriedade [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) para um objeto **Recordset** ativo e retorna um erro. O erro ocorre independentemente de a página ser proveniente de um site da Web registrado na lista de sites confiáveis.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>Alterações na manipulação de provedores de OLE DB e segurança integrada
 Ao examinar o ADO 2,7 e versões anteriores para problemas potenciais de segurança e preocupações, o seguinte cenário foi descoberto:

 Em alguns casos, OLE DB provedores que dão suporte à propriedade de [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) de segurança integrada podem potencialmente permitir que páginas da Web com script reutilizem o objeto de conexão ADO para se conectarem de forma não intencional a outros servidores usando as credenciais de logon atuais dos usuários. Para evitar isso, o ADO 2,8 e versões posteriores manipulam OLE DB provedores dependendo de como eles optaram por fornecer ou não fornecer, para segurança integrada.

 Para páginas da Web que são carregadas de sites listados na lista de zona de sites confiáveis, a tabela a seguir fornece uma análise de como o ADO 2,8 e posterior gerencia as conexões do ADO em cada caso.

|Configurações do IE para autenticação de usuário, logon|O provedor dá suporte a "segurança integrada" e UID e PWD são especificados (SQLOLEDB)|O provedor não dá suporte a "segurança integrada" (JOLT, MSDASQL, MSPersist)|O provedor dá suporte a "segurança integrada" e está definido como SSPI (nenhum UID/PWD está especificado)|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Logon automático com nome de usuário e senha atuais|Permitir conexão|Permitir conexão|Permitir conexão|
|Solicitar nome de usuário e senha|Permitir conexão|Falha na conexão|Falha na conexão|
|Logon automático somente na zona da intranet|Permitir conexão|Avisar o usuário com aviso de segurança|Avisar o usuário com aviso de segurança|
|Logon anônimo|Permitir conexão|Falha na conexão|Falha na conexão|

 No caso em que um aviso de segurança agora aparece, a caixa de mensagem informa os usuários:

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 A mensagem anterior permite que o usuário tome uma decisão mais informada e continue de acordo.

> [!NOTE]
>  Para sites não confiáveis (ou seja, sites não listados na lista de zona de sites confiáveis), se o provedor também não for confiável (como discutido anteriormente nesta seção), o usuário poderá ver dois avisos de segurança em uma linha, um aviso sobre o provedor não seguro e um segundo aviso sobre a tentativa de usar sua identidade. Se o usuário clicar em OK para o primeiro aviso, as configurações do Internet Explorer e o código de comportamento de resposta descritos na tabela anterior serão executados.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>Controlando se o texto da senha é retornado nas cadeias de conexão ADO
 Quando você tenta obter o valor da propriedade [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) em um objeto de **conexão** ADO, ocorrem os seguintes eventos:

1.  Se a conexão estiver aberta, uma chamada de inicialização será feita para o provedor de OLE DB subjacente para obter a cadeia de conexão.

2.  Dependendo da configuração no provedor de OLE DB da propriedade [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) , as senhas são incluídas junto com outras informações de cadeia de conexão que são retornadas.

 Por exemplo, se a propriedade dinâmica de conexão ADO **manter informações de segurança** estiver definida como **true**, as informações de senha serão incluídas na cadeia de conexão retornada. Caso contrário, se o provedor subjacente tiver definido a propriedade como **false** (por exemplo, com o provedor SQLOLEDB), as informações de senha serão omitidas na cadeia de conexão retornada.

 Se você estiver usando provedores de terceiros (que não são da Microsoft) OLE DB com o código do aplicativo ADO, poderá verificar como a propriedade **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** é implementada para determinar se a inclusão de informações de senha com cadeias de conexão ADO é permitida.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>Verificando dispositivos que não são de arquivo ao carregar e salvar conjuntos de registros ou fluxos
 Para o ADO 2,7 e anterior, as operações de entrada/saída de arquivo, como [abrir](../../ado/reference/ado-api/open-method-ado-recordset.md) e [salvar](../../ado/reference/ado-api/save-method.md) , que foram usadas para ler e gravar dados baseados em arquivo, podem, em alguns casos, permitir que uma URL ou nome de arquivo seja usado, o que especificou um tipo de arquivo não baseado em disco. Por exemplo, LPT1, COM2, PRN. TXT, a AUX pode ser usada como um alias para entrada/saída entre impressoras e dispositivos auxiliares no sistema usando determinados

 Para o ADO 2,8 e posterior, essa funcionalidade foi atualizada. Para abrir e salvar objetos **Recordset** e **Stream** , o ADO agora executa uma verificação de tipo de arquivo para garantir que o dispositivo de entrada ou saída especificado em uma URL ou nome de arquivo seja um arquivo real.

> [!NOTE]
>  A verificação de tipo de arquivo conforme descrito nesta seção se aplica somente ao Windows 2000 e posterior. Ele não se aplica a situações em que o ADO 2,8 ou posterior está sendo executado em versões anteriores do Windows, como o Windows 98.
