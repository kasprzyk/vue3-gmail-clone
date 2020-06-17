<template>
  <table class="mail-table">
    <tbody>
      <tr
        v-for="email in unarchivedEmails"
        :key="email.id"
        :class="['clickable', email.read ? 'read' : '']"
        @click="email.read = true"
      >
        <td>
          <input type="checkbox" />
        </td>
        <td>{{ email.from }}</td>
        <td>
          <p>
            <strong>{{ email.subject }}</strong> - {{ email.body }}
          </p>
        </td>
        <td class="date">{{ format(new Date(email.sentAt), "MMM do yyyy") }}</td>
        <td><button @click="email.archived = true">Archive</button></td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import { format } from "date-fns";

export default {
  async setup() {
    await new Promise(resolve => setTimeout(resolve, 3000));
    return {
      format,
      emails: [
        {
          id: 1,
          from: "piotkas1@gmail.com",
          subject: "test",
          body: "test",
          sentAt: "2020-03-27T18:25:43.511Z",
          archived: false,
          read: true
        },
        {
          id: 2,
          from: "piotkas1@gmail.com",
          subject: "test",
          body: "test",
          sentAt: "2020-03-27T18:25:43.511Z",
          archived: false,
          read: false
        },
        {
          id: 3,
          from: "piotkas1@gmail.com",
          subject: "test",
          body: "test",
          sentAt: "2020-03-27T18:25:43.511Z",
          archived: false,
          read: false
        },
        {
          id: 4,
          from: "piotkas1@gmail.com",
          subject: "test",
          body: "test test test test test",
          sentAt: "2020-03-27T18:25:43.511Z",
          archived: true,
          read: false
        }
      ]
    };
  },
  computed: {
    sortedEmails() {
      return this.emails.sort((e1, e2) => {
        return e1.sentAt < e2.sentAt ? 1 : -1;
      });
    },
    unarchivedEmails() {
      return this.sortedEmails.filter(e => !e.archived);
    }
  }
};
</script>
