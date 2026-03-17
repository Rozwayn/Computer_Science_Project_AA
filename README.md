# Inn ‘n Out: A Digital Leave Pass System for Pisay Dormers

## Project Description
Our project’s general objective is to develop a computerized system that processes dormers’ leave passes efficiently in order to reduce long queues, rushing, and manual paperwork every Sunday and Friday.



## Specific Objectives
- Enable dormers to submit leave passes digitally instead of lining up in person.
- Reduce the average processing time of leave slips compared to the manual method.
- Allow dorm staff to browse dormers’ leave passes through the system.
- Automatically store and organize leave pass records in a database.
- Generate a list or report of approved and pending leave requests.
- Minimize errors caused by handwritten or manually recorded passes.
- Provide a searchable record of dormers’ leave history.



## Core Features (Must-Have)

### User Registration and Login
- Dormers and dorm staff can register and log in using email and password.
- Ensures only authorized users can access the system and perform assigned roles.

### Role-Based Access (Dormer and Dorm Staff)
- After login, users are directed to dashboards based on their role.
- Dormers can submit and view leave passes.
- Dorm staff can review, approve, or reject submitted requests.

### Digital Leave Pass Submission
- Dormers enter details: date of leave, time out, expected time in, and reason.
- Eliminates manual forms and long queues.

### Leave Pass Review and Approval
- Dorm staff can approve or reject submitted leave passes.
- Provides organized and faster processing.

### Leave Pass Status Tracking
- Displays status of each leave pass (Pending, Approved, Rejected).
- Helps dormers monitor requests without asking in person.

### Automatic Record Saving
- All submissions and updates are automatically saved.
- Records are organized and available for future reference.



## Pseudocode
START
DISPLAY Welcome Screen DISPLAY Login / Register Option
IF user selects Register THEN INPUT name, email, password, role SAVE user information DISPLAY Registration Successful END IF
IF user selects Login THEN INPUT email, password
IF credentials are valid THEN
    IF role = Dormer THEN
        DISPLAY Dormer Dashboard
    ELSE IF role = Dorm Staff THEN
        DISPLAY Dorm Staff Dashboard
    END IF
ELSE
    DISPLAY Invalid Login Message
    RETURN to Welcome Screen
END IF
END IF
// DORMER FUNCTIONS IF user role = Dormer THEN DISPLAY list of submitted leave passes and their status
IF dormer selects Submit Leave Pass THEN
    INPUT date of leave, time out, expected time in, reason
    SET status = "Pending"
    SAVE leave pass record
    DISPLAY Submission Successful
END IF
END IF
// DORM STAFF FUNCTIONS IF user role = Dorm Staff THEN DISPLAY list of submitted leave passes with details
IF staff selects a leave pass THEN
    DISPLAY leave pass details

    IF staff clicks Approve THEN
        SET status = "Approved"
        UPDATE record
        DISPLAY Approval Successful

    ELSE IF staff clicks Reject THEN
        SET status = "Rejected"
        INPUT rejection reason
        UPDATE record
        DISPLAY Rejection Message
    END IF
END IF
END IF
DISPLAY updated dashboards
END
Copy code



## Members
- 21 Nambio, Enricha Gemm  
- 22 Pedernal, Lucas Inigo  
- 23 Privado, Louise Janine  
- 24 Rafael, Roswyn Drawde  
- 25 Reyes, Auric Geranyl  

---

## Program System (Final C++ Code)

```cpp
#include <iostream>
#include <string>
using namespace std;

const int MAX = 100;

struct LeavePass {
    string dormerName;
    string dormerEmail;
    string date;
    string timeOut;
    string expectedTimeIn;
    string reason;
    string status; // Pending / Approved / Rejected
    string rejectionReason;
};

int main() {
    int login;
    string loginname, loginemail, loginpassword;
    int loginrole;
    int leavepass;

    LeavePass leavePasses[MAX];
    int totalLeavePass = 0;

    cout << "=== Welcome to Inn 'n Out Leave Pass System ===" << endl;

    while(true) {
        cout << "\nLogin (1 = yes, 2 = no)? ";
        cin >> login;
        cin.ignore();

        if(login == 2) {
            cout << "Program Closed." << endl;
            break;
        }

        if(login == 1) {
            cout << "Enter Name: ";
            getline(cin, loginname);
            cout << "Enter Email: ";
            getline(cin, loginemail);
            cout << "Enter Password: ";
            getline(cin, loginpassword);
            cout << "Enter Role (1 = Dormer, 2 = Staff): ";
            cin >> loginrole;
            cin.ignore();

            if(loginrole == 1) { // Dormer
                cout << "\nWelcome Dormer " << loginname << "!" << endl;
                cout << "Submit Leave Pass (1 = yes, 2 = no)? ";
                cin >> leavepass;
                cin.ignore();

                if(leavepass == 1) {
                    LeavePass newPass;
                    newPass.dormerName = loginname;
                    newPass.dormerEmail = loginemail;
                    newPass.status = "Pending";

                    cout << "Enter Date of Leave: ";
                    getline(cin, newPass.date);
                    cout << "Enter Time Out: ";
                    getline(cin, newPass.timeOut);
                    cout << "Enter Expected Time In: ";
                    getline(cin, newPass.expectedTimeIn);
                    cout << "Enter Reason: ";
                    getline(cin, newPass.reason);

                    leavePasses[totalLeavePass] = newPass;
                    totalLeavePass++;

                    cout << "Leave Pass Submitted Successfully!" << endl;
                    cout << "Total Leave Passes Today: " << totalLeavePass << endl;
                } else {
                    cout << "No Leave Pass Submitted." << endl;
                }
            }

            else if(loginrole == 2) { // Staff
                cout << "\nWelcome Staff " << loginname << "!" << endl;

                if(totalLeavePass == 0) {
                    cout << "No leave passes recorded." << endl;
                } else {
                    for(int i = 0; i < totalLeavePass; i++) {
                        cout << "\nDormer #" << i + 1 << endl;
                        cout << "Name: " << leavePasses[i].dormerName << endl;
                        cout << "Email: " << leavePasses[i].dormerEmail << endl;
                        cout << "Date: " << leavePasses[i].date << endl;
                        cout << "Time Out: " << leavePasses[i].timeOut << endl;
                        cout << "Expected Time In: " << leavePasses[i].expectedTimeIn << endl;
                        cout << "Reason: " << leavePasses[i].reason << endl;
                        cout << "Status: " << leavePasses[i].status << endl;

                        if(leavePasses[i].status == "Pending") {
                            int decision;
                            cout << "Approve (1) / Reject (2) / Skip (3): ";
                            cin >> decision;
                            cin.ignore();

                            if(decision == 1) {
                                leavePasses[i].status = "Approved";
                                cout << "Leave Pass Approved." << endl;
                            } else if(decision == 2) {
                                leavePasses[i].status = "Rejected";
                                cout << "Enter Rejection Reason: ";
                                getline(cin, leavePasses[i].rejectionReason);
                                cout << "Leave Pass Rejected." << endl;
                            } else {
                                cout << "Skipped." << endl;
                            }
                        }
                    }
                }
            }

            else {
                cout << "Invalid Role." << endl;
            }
        } else {
            cout << "Invalid choice." << endl;
        }
    }

    return 0;
}
