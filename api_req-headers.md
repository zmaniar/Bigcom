###Request Headers

<table class="bui-table"><thead><tr>
<th class="headers-name"> Header </th>
<th class="headers-values"> Allowed Values </th>
<th class="headers-description"> Description </th>
<th class="headers-example"> Example </th>
</tr></thead><tbody>

<tr>
<td><p> <code><b>Accept</b></code>  </p></td>
<td><p> <code><b>application/json</b></code> (for .json requests) 
<code><b>application/xml</b></code> (for .xml requests)  </p></td>
<td><p> The MIME type for the format you want to receive a response in. </p></td>
<td><p> <code><b>application/xml</b></code>  </p></td>
</tr>
<tr>
<td><p> <code><b>Authorization</b></code></p></td>
<td><p> <code><b>Basic</b></code>  </p></td>
<td><p> The user credentials for accessing the API</p></td>
<td><p> <code><b>Basic&nbsp;YWRtaW46cGFzc3dvcmQ=</b></code>  </p></td>
</tr>
<tr>
<td><p> <code><b>Content-Type</b></code>  </p></td>
<td><p> <code><b>application/json</b></code> (for JSON requests) 
<code><b>application/xml</b></code> (for XML requests)  </p></td>
<td><p> The MIME type of the request body. Use to validate and parse the request to the API. </p></td>
<td><p> <code><b>application/json</b></code> </p></td>
</tr>
<tr>
<td><p> <code><b>User-Agent</b></code> </p></td>
<td><p> String </p></td>
<td><p> While it is not required, we ask that you specify a user agent which identifies your integration/client with your requests. </p></td>
<td><p>&nbsp;</p></td>
</tr>
<tr>
<td><p> <code><b>X-Auth-Client</b></code> </p></td>
<td><p> String </p></td>
<td><p> Client ID of the requesting app</p></td>
<td><p>&nbsp;</p></td>
</tr>
<tr>
<td><p> <code><b>X-Auth-Token</b></code> </p></td>
<td><p> String </p></td>
<td><p> Access token authorizing the app to access resources on behalf of a user</p></td>
<td><p>&nbsp;</p></td>
</tr>
</tbody>
</table>

<h3>Deprecated Headers</h3>

<p>The following headers are deprecated and will eventually be removed from the API.</p>

<table class="bui-table"><thead><tr>
<th class="headers-name"> Header </th>
<th class="headers-description"> Description </th>
<th class="headers-example"> Use Instead</th>
</tr></thead><tbody>
<tr>
<td><p> <code><b>If-Modified-Since</b></code> </p></td>
<td><p> Uses an <a href="http://tools.ietf.org/html/rfc2822#section-3.3" class="external-link" rel="nofollow">RFC 2822</a> date. If supplied, then only resources modified since the specified date will be returned. If there are no modified objects, then a <code><b>304 Not Modified</b></code> response will be sent. Please refer to the individual resource pages for support for this header. </p></td>
<td><p>Use <b>min_date_modified</b> and 
<b>max_date_modified</b> query parameters on resources that support them.</p></td>
</tr>
</tbody>
</table>
