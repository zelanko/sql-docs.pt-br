---
title: Escrevendo seu próprio manipulador personalizado | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
- customized handler in RDS [ADO]
ms.assetid: d447712a-e123-47b5-a3a4-5d366cfe8d72
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b9cb903d276357e46489dbdcd316d4f3974087a
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35274695"
---
# <a name="writing-your-own-customized-handler"></a>Escrevendo seu próprio manipulador personalizado
Talvez você queira gravar seu próprio manipulador se você for um administrador de servidor do IIS que deseja que o padrão de suporte de RDS, mas mais controle sobre solicitações de usuários e direitos de acesso.  
  
 MSDFMAP. Manipulador implementa o **IDataFactoryHandler** interface.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="idatafactoryhandler-interface"></a>Interface IDataFactoryHandler  
 Essa interface possui dois métodos, **GetRecordset** e **reconectar**. Ambos os métodos requerem que o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade ser definida como **adUseClient**.  
  
 Ambos os métodos usam argumentos que apareçam depois da vírgula primeiro no "**manipulador =**" palavra-chave. Por exemplo, `"Handler=progid,arg1,arg2;"` irá passar uma cadeia de caracteres do argumento de `"arg1,arg2"`, e `"Handler=progid"` irá passar um argumento nulo.  
  
## <a name="getrecordset-method"></a>Método GetRecordset  
 Este método consulta a fonte de dados e cria um novo [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto usando os argumentos fornecidos. O **registros** deve ser aberto com **adLockBatchOptimistic** e não deve ser aberto de forma assíncrona.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** a cadeia de caracteres de conexão.  
  
 ***argumentos*** os argumentos para o manipulador.  
  
 ***consulta*** o texto de comando para fazer uma consulta.  
  
 ***ppRS*** o ponteiro onde o **registros** devem ser retornados.  
  
## <a name="reconnect-method"></a>Reconectar-se o método  
 Este método atualiza a fonte de dados. Cria um novo [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) objeto e anexa o determinado **registros**.  
  
### <a name="arguments"></a>Argumentos  
 ***conn*** a cadeia de caracteres de conexão.  
  
 ***argumentos*** os argumentos para o manipulador.  
  
 ***pRS*** um **registros** objeto.  
  
## <a name="msdfhdlidl"></a>msdfhdl.idl  
 Esta é a definição de interface para **IDataFactoryHandler** que aparece no **msdfhdl.idl** arquivo.  
  
```  
[  
  uuid(D80DE8B3-0001-11d1-91E6-00C04FBBBFB3),  
  version(1.0)  
]  
library MSDFHDL  
{  
    importlib("stdole32.tlb");  
    importlib("stdole2.tlb");  
  
    // TLib : Microsoft ActiveX Data Objects 2.0 Library  
    // {00000200-0000-0010-8000-00AA006D2EA4}  
    #ifdef IMPLIB  
    importlib("implib\\x86\\release\\ado\\msado15.dll");  
    #else  
    importlib("msado20.dll");  
    #endif  
  
    [  
      odl,  
      uuid(D80DE8B5-0001-11d1-91E6-00C04FBBBFB3),  
      version(1.0)  
    ]  
    interface IDataFactoryHandler : IUnknown  
    {  
HRESULT _stdcall GetRecordset(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] BSTR query,  
      [out, retval] _Recordset **ppRS);  
  
// DataFactory will use the ActiveConnection property  
// on the Recordset after calling Reconnect.  
   HRESULT _stdcall Reconnect(  
      [in] BSTR conn,  
      [in] BSTR args,  
      [in] _Recordset *pRS);  
    };  
};  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de personalização de conectar-se a seção](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção do arquivo UserList de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)


