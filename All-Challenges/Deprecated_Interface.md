# Deprecated Interface

**Category**: Security Misconfiguration  
**Difficulty**: 2

**Description**:  
A deprecated B2B interface for uploading invoice or order files was not properly shut down and is still active in the application. This interface accepts specific file formats and can be triggered through a functionality that's still available in the frontend, though its purpose is no longer clearly advertised.

---

**Solution**:  
The solution was achieved by discovering the inactive, but still functioning, B2B invoice upload functionality through a file input field in the "Customer Feedback / Complaint" section. Despite frontend restrictions suggesting only `.pdf` and `.zip` files are accepted, the application backend also accepted `.xml` files, which are typically used in B2B EDI (Electronic Data Interchange) formats.

---

**Steps**:

1. Navigated to:
   
   ```
   http://localhost:3000/#/complain
   ```

2. Noticed that the file upload input only accepted `.pdf` and `.zip` files based on the UI.

3. Opened **DevTools → Elements**, searched for the input element and located the label:
   
   ```
   Input area for uploading a single invoice PDF or XML B2B order file or a ZIP archive containing multiple invoices or orders
   ```

4. This hinted that `.xml` might also be accepted by the backend, even though it's not advertised or allowed by the client-side file input restrictions.

5. Used the file input field to upload a random `.xml` file.

6. After submission, the application accepted the file, and the challenge **Deprecated Interface** was immediately marked as solved.

---

**Note**:  
This challenge highlights a typical security misconfiguration: backend functionality (in this case, a deprecated B2B XML upload endpoint) remains active despite being removed from visible UI paths. Legacy systems often leave such backdoors unintentionally open.

---

**Challenge solved!** was triggered by successfully uploading a `.xml` file via the complaint form.
