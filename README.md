# GMAIL_ATTACHMENT
### Code Description:

This script uses the **`ezgmail`** library to interact with Gmail accounts, specifically to search for emails that have attachments and then allow the user to download those attachments. Below is a step-by-step breakdown of how the code works:

---

#### 1. **Imports:**
```python
import ezgmail
```
- The script imports the `ezgmail` library, which is used for accessing Gmail data and interacting with Gmail APIs to perform various actions like searching emails and downloading attachments.

---

#### 2. **Function: `attachmentdownload(result_threads)`**
```python
def attachmentdownload(result_threads):
    """
    Downloads all attachments from the given Gmail threads.
    Each thread may contain multiple messages.
    """
```
- This function is designed to download all attachments from the Gmail threads passed as `result_threads`.
- It loops through each thread and then checks for individual messages within that thread. For each message, it downloads any attachments.

```python
    try:
        for thread in result_threads:
            for message in thread.messages:
                message.downloadAllAttachments()
        print("✅ Download complete. Please check your Downloads or working directory.")
    except Exception as e:
        print("❌ Error occurred while downloading attachments:", e)
```
- It uses the `downloadAllAttachments()` method from `ezgmail` to download all the attachments in the message.
- If successful, it prints a success message: `"✅ Download complete"`.
- If there's an error during the process, it catches the exception and prints an error message with the exception details.

---

#### 3. **Main Logic:**
```python
if __name__ == '__main__':
    query = input("🔎 Enter search query: ")
```
- This is the main part of the script that runs when executed.
- It asks the user to input a **search query** (like "invoice" or "report"). This query is used to search Gmail for emails that match the user's input.

```python
    new_query = query + " has:attachment"
```
- The code appends `has:attachment` to the user's query to ensure only emails with attachments are searched.
  
```python
    result_threads = ezgmail.search(new_query)
```
- The `ezgmail.search()` method performs the search on Gmail using the **new query** (which includes both the user’s input and the attachment filter).

---

#### 4. **Processing Results:**
```python
    if not result_threads:
        print("❌ No results with attachments found.")
```
- If there are no results (i.e., no threads with attachments), it will print a message saying no attachments were found.

```python
    else:
        print("\n📬 Result(s) with attachments found:\n")
        for thread in result_threads:
            print(f"📩 Email Subject: {thread.messages[0].subject}")
```
- If results are found, it prints a message indicating that attachments were found, followed by the subject of each email thread with attachments.

---

#### 5. **User Input for Downloading Attachments:**
```python
        ask = input("\n💾 Do you want to download these attachments? (Yes/No): ").strip().lower()
        if ask == "yes":
            attachmentdownload(result_threads)
        else:
            print("🛑 Download canceled by user.")
```
- After displaying the search results, the script asks the user whether they want to **download** the attachments.
- If the user inputs `"yes"`, it calls the `attachmentdownload(result_threads)` function to download the attachments.
- If the user inputs `"no"`, the script exits with the message `"Download canceled by user."`

---

### ✅ **Summary:**
- This script allows the user to search their Gmail account for emails that contain attachments.
- It displays the subjects of the emails found and prompts the user to decide if they want to download the attachments.
- If the user agrees, it downloads all attachments from the emails in the search result.
